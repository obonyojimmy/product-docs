Ensembl System API
!!!!!!!!!!!!!!!!!!!

Ensembl is a genome browser for vertebrate genomes that supports research in comparative genomics, evolution, sequence variation and transcriptional regulation. Ensembl annotate genes, computes multiple alignments, predicts regulatory function and collects disease data. Ensembl tools include BLAST, BLAT, BioMart and the Variant Effect Predictor (VEP) for all supported species.

The figure below shows a summary of Ensembl functions:

.. image:: /_static/Ensembl-summary.png

**API Instructions Summary (tl;dr)**

This will be a process API for a biology database called Ensembl that we have hosted on AWS. The purpose will be to import a .vcf file stored in an S3 bucket and run the “Variant Effect Predictor” workflow on it, then store the output as a file back in the same S3 bucket. A high-level diagram is shown below:

.. image:: /_static/Ensembl-api-overview.png

Process steps:

* The API will first need to pull a .vcf file from an AWS S3 endpoint and transfer it to the AWS EC2 Ensembl endpoint. At this point no queuing is needed but we will add queuing in the future
* The API then needs to call the Ensembl Variant Effect Predictor Workflow. This will annotate the file and produce a new file as an output
* The API should handle errors that occur during this process and retry as needed to a reasonable point. 
* We will also need to watch for the successful completion of the process and make sure a new annotated output file has been created
* The output file will be transferred back to the S3 endpoint and stored. Note that the file transfer and storage should not be a blocker. As this API will interact with many other APIs, the file handling piece is not nearly as important as the data processing piece. As long as the data are ingested, processed, and transformed, the transfer and storage are of lower priority.

Connection instructions:
Stored here as soon as we make the docs private.

Methods and Requirements

* This must be written as a REST API
* This must follow the format and standards defined in the existing API templates located here: https://bitbucket.org/snippetmd/snippet-api-platform
* All code must be documented. We use readthedocs for our documentation, so your documentation may be in sphinx/markdown language or plain text. See more about the documentation here: http://docs.readthedocs.io/en/latest/getting_started.html


**Data Inputs**
@@@@@@@@@@@@@@@

The input data should be assumed to be in a GA4GH-compatible format. If any new fields are added for inputs and outputs, their format should be matched as closely as possible to the GA4GH schema and they should be noted here. 

The default input format for Ensembl data is a simple whitespace-separated format (columns may be separated by space or tab characters), containing five required columns plus an optional identifier column. We will access the data programmatically through the API, so the inputs should be JSON or XML transformed from the GA4GH format to Ensembl-compatible format using Groovy. We will use the Variant Effect Predictor tool in Ensembl. The five required data elements with optional identifier are:

**Required**

* Chromosome - just the name or number, with no 'chr' prefix. I believe the GA4GH schema map item is Variant:reference_name(string), but this will need to be validated. 
* Start - the start position at which the variant occurs. Note that GA4GH uses Variant:start(long), a 0-based numbering item (the numbering starts at 0 instead of 1 for the first item). This is relatively unusual in the biological world and will need to be validated to ensure it doesn't cause problems when matching with other systems. This corresponds to the first base of the string of reference bases. Genomic positions are non-negative integers less than reference length. Variants spanning the join of circular genomes are represented as two variants one on each side of the join (position 0).
* End - the end position (exclusive), resulting in (start, end) closed-open interval. This is typically calculated in GA4GH as start + referenceBases.length. Defined in GA4GH as Variant:end(long).
* Allele - pair of alleles separated by a '/', with the reference allele first. This will need to be explored in the GA4GH documentation. Usually this is represented as something like "*19/*19" - the full variant would include the allele annotation and is ususally represented as Gene+allele, or "CYP2C9 *19/*19"
* Strand - defined as + (forward) or - (reverse). The match for this in GA4GH will need to be researched.
* Optional identifier - this identifier will be used in Variant Effect Predictor's (VEP)'s output. If not provided, VEP will construct an identifier from the given coordinates and alleles.

**Data Outputs**
@@@@@@@@@@@@@@@@

For now, the output format (JSON/XML) is unimportant. The important thing is that the output is transformed into the GA4GH standard with Groovy.

**Required**

* Allele - the variant allele used to calculate the consequence
* Gene - Ensembl stable ID of affected gene
* Feature - Ensembl stable ID of feature
* Consequence - consequence type of this variant
* Amino acid change - only given if the variant affects the protein-coding sequence
* Amino acid change - only given if the variant affects the protein-coding sequence
* IMPACT - the impact modifier for the consequence type
* VARIANT_CLASS - Sequence Ontology variant class
* ExAC_Adj_AF - Adjusted frequency of existing variant in ExAC combined population
* CLIN_SIG - ClinVar clinical significance of the dbSNP variant
* BIOTYPE - Biotype of transcript or regulatory feature
* APPRIS - Annotates alternatively spliced transcripts as primary or alternate based on a range of computational methods. NB: not available for GRCh37
* PUBMED - Pubmed ID(s) of publications that cite existing variant
* SOMATIC - Somatic status of existing variant(s)
* PHENO - Indicates if existing variant is associated with a phenotype, disease or trait
* GENE_PHENO - Indicates if overlapped gene is associated with a phenotype, disease or trait
* REFSEQ_MATCH - the RefSeq transcript match status; contains a number of flags indicating whether this RefSeq transcript matches the underlying reference sequence and/or an Ensembl transcript (more information). NB: not available for GRCh37.


**Available but not used**

* Uploaded variation - as chromosome_start_alleles
* Location - in standard coordinate format (chr : start or chr : start-end)
* Feature type - type of feature. Currently one of Transcript, RegulatoryFeature, MotifFeature
* Position in cDNA - relative position of base pair in cDNA sequence
* Position in CDS - relative position of base pair in coding sequence
* Position in protein - relative position of amino acid in protein
* Codon change - the alternative codons with the variant base in upper case
* Extra - this column contains extra information as key=value pairs separated by ";", see below.
* SYMBOL - the gene symbol
* SYMBOL_SOURCE - the source of the gene symbol
* STRAND - the DNA strand (1 or -1) on which the transcript/feature lies
* ENSP - the Ensembl protein identifier of the affected transcript
* FLAGS - transcript quality flags:
cds_start_NF: CDS 5' incomplete
cds_end_NF: CDS 3' incomplete
* SWISSPROT - Best match UniProtKB/Swiss-Prot accession of protein product
* TREMBL - Best match UniProtKB/TrEMBL accession of protein product
* UNIPARC - Best match UniParc accession of protein product
* HGVSc - the HGVS coding sequence name
* HGVSp - the HGVS protein sequence name
* HGVSg - the HGVS genomic sequence name
* HGVS_OFFSET - Indicates by how many bases the HGVS notations for this variant have been shifted
* NEAREST - Identifier(s) of nearest transcription start site
* SIFT - the SIFT prediction and/or score, with both given as prediction(score)
* PolyPhen - the PolyPhen prediction and/or score
* MOTIF_NAME - the source and identifier of a transcription factor binding profile aligned at this position
* MOTIF_POS - The relative position of the variation in the aligned TFBP
* HIGH_INF_POS - a flag indicating if the variant falls in a high information position of a transcription factor binding profile (TFBP)
* MOTIF_SCORE_CHANGE - The difference in motif score of the reference and variant sequences for the TFBP
* CELL_TYPE - List of cell types and classifications for regulatory feature
* CANONICAL - a flag indicating if the transcript is denoted as the canonical transcript for this gene
* CCDS - the CCDS identifer for this transcript, where applicable
* INTRON - the intron number (out of total number)
* EXON - the exon number (out of total number)
* DOMAINS - the source and identifer of any overlapping protein domains
* DISTANCE - Shortest distance from variant to transcript
* IND - individual name
* ZYG - zygosity of individual genotype at this locus
* SV - IDs of overlapping structural variants
* FREQS - Frequencies of overlapping variants used in filtering
* AF - Frequency of existing variant in 1000 Genomes
* AFR_AF - Frequency of existing variant in 1000 Genomes combined African population
* AMR_AF - Frequency of existing variant in 1000 Genomes combined American population
* ASN_AF - Frequency of existing variant in 1000 Genomes combined Asian population
* EUR_AF - Frequency of existing variant in 1000 Genomes combined European population
* EAS_AF - Frequency of existing variant in 1000 Genomes combined East Asian population
* SAS_AF - Frequency of existing variant in 1000 Genomes combined South Asian population
* AA_AF - Frequency of existing variant in NHLBI-ESP African American population
* EA_AF - Frequency of existing variant in NHLBI-ESP European American population
* ExAC_AF - Frequency of existing variant in ExAC combined population
* ExAC_AFR_AF - Frequency of existing variant in ExAC African/American population
* ExAC_AMR_AF - Frequency of existing variant in ExAC American population
* ExAC_EAS_AF - Frequency of existing variant in ExAC East Asian population
* ExAC_FIN_AF - Frequency of existing variant in ExAC Finnish population
* ExAC_NFE_AF - Frequency of existing variant in ExAC Non-Finnish European population
* ExAC_OTH_AF - Frequency of existing variant in ExAC combined other combined populations
* ExAC_SAS_AF - Frequency of existing variant in ExAC South Asian population
* MAX_AF - Maximum observed allele frequency in 1000 Genomes, ESP and ExAC
* MAX_AF_POPS - Populations in which maximum allele frequency was observed
* TSL - Transcript support level. NB: not available for GRCh37
* ALLELE_NUM - Allele number from input; 0 is reference, 1 is first alternate etc
* MINIMISED - Alleles in this variant have been converted to minimal representation before consequence calculation
* PICK - indicates if this block of consequence data was picked by --flag_pick or --flag_pick_allele