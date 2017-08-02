Ensembl System API
!!!!!!!!!!!!!!!!!!!

Ensembl is a genome browser for vertebrate genomes that supports research in comparative genomics, evolution, sequence variation and transcriptional regulation. Ensembl annotate genes, computes multiple alignments, predicts regulatory function and collects disease data. Ensembl tools include BLAST, BLAT, BioMart and the Variant Effect Predictor (VEP) for all supported species.

The figure below shows a summary of Ensembl functions:

.. image:: /_static/Ensembl-summary.png


**Data Inputs**
@@@@@@@@@@@@@@@

The default format for the web app is a simple whitespace-separated format (columns may be separated by space or tab characters), containing five required columns plus an optional identifier column. We will access the data programmatically through the API. The five required data elements with optional identifier are:

**Required**

* Chromosome - just the name or number, with no 'chr' prefix
* Start
* End
* Allele - pair of alleles separated by a '/', with the reference allele first
* Strand - defined as + (forward) or - (reverse).
* Optional identifier - this identifier will be used in VEP's output. If not provided, VEP will construct an identifier from the given coordinates and alleles.

**Data Outputs**
@@@@@@@@@@@@@@@@

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