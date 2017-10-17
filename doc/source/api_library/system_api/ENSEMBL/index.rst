Ensembl System API
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

Ensembl is a genome browser for vertebrate genomes that supports research in comparative genomics, evolution, sequence variation and transcriptional regulation. Ensembl annotate genes, computes multiple alignments, predicts regulatory function and collects disease data. Ensembl tools include BLAST, BLAT, BioMart and the Variant Effect Predictor (VEP) for all supported species.

The figure below shows a summary of Ensembl functions:

.. image:: /_static/Ensembl-summary.png

**API Instructions Summary (tl;dr)**

This will be a process API for a biology database called Ensembl that we have hosted on AWS. The purpose will be to use some variant information parsed from the Galaxy vcf output and run “Variant Effect Predictor” workflows on it, then store the output for future analysis.

Connection instructions:
Stored here as soon as we make the docs private.

Methods and Requirements

* This must be written as a REST API
* All code must be documented. We use readthedocs for our documentation, so your documentation may be in sphinx/markdown language or plain text. See more about the documentation here: http://docs.readthedocs.io/en/latest/getting_started.html


**Data Inputs**
@@@@@@@@@@@@@@@

The input data should be assumed to be in a GA4GH-compatible format. If any new fields are added for inputs and outputs, their format should be matched as closely as possible to the GA4GH schema and they should be noted here. 

**Required**

We will use the output data from Galaxy as the input data for Ensembl. The Galaxy output will have several key fields we will use:

#. Chromosome (Galaxy ID: CHROM; Ensembl ID: chromosome) this is simply the chromosome number, represented as an integer - e.g. 1
#. Start (Galaxy ID: POS; Ensembl ID: start): this is the start position of the variant on the chromosome, and will be an integer - e.g. 881907
#. End (Galaxy ID: none - not a direct output of galaxy, this will be a calculated field; Ensembl ID: end): this is the end position of the variant on the chromosome, and will generally equal the start position with some exceptions. The logic is as follows:

Logic:
Ignore "." ("." = 0)
IF ALT = ".", "POS" + NUMBER OF CHARACTERS IN "REF" - 1 
ELSE "POS" + NUMBER OF CHARACTERS IN "ALT" - NUMBER OF CHARACTERS(A,C,G,T) IN "REF." 

Example: 
POS (start) = 56000
REF = A 
ALT = AGAT 
End = start + length(ALT) - length(REF) = 56000 + 4 - 1 = 56003

#. Allele (Galaxy ID: none - not a direct output of galaxy, this will be a calculated field; Ensembl ID: allele): This is a description of the allele, how each amino acid in the expected sequence is replaced with something else. The logic is as follows:

Logic:
FIRST REPLACE ALL "." WITH "-"
THEN IF NUMBER OF CHARACTERS IN "ALT" > NUMBER OF CHARACTERS IN "REF" AND THE FIRST CHARACTER OF EACH IS THE SAME, IGNORE THE FIRST CHARACTER. THEN ALLELE = "REF" & "/" & "ALT" WITH THE LEADING CHARACTER REMOVED.
OTHERWISE ALLELE = "REF" & "/" & "ALT"

Example 1:
REF = G
ALT = C
Allele = G/C

Example 2:
REF = A
ALT = AGAT
Allele = -/GAT

Example 3:
REF = GAT
ALT = .
Allele = GAT/-

Example 4:
REF = G
ALT = CAGT
Allele = G/CAGT

#. Strand (Galaxy ID: none, not a direct output out of galaxy; Ensembl ID = strand): this is defined as either forward (+) or reverse (-). For our purposes, Galaxy has already standardized the output for us. This value will always be "+".

We will pass the following variables into the Ensembl Variant Effect Predictor:

* chromosome (e.g. 1)
* start (e.g. 881907)
* end (e.g. 881906)
* allele (e.g. -/C)
* strand (e.g. +)

**Data Outputs**
@@@@@@@@@@@@@@@@

For now, the output format (JSON/XML) is unimportant. The important thing is that the output is transformed into the GA4GH standard with Groovy.

**Required**

* dbSNP HGVS IDs : for example, NM_174936.3:c.137G>A , ...
* EXTERNAL:External References, EntrezGene ID
* Phenotype Data : Significant Associations : Phenotype, disease and trait - e.g. Breat-ovarian cancer, familial 2
* Phenotype Data : Significant Associations : Clinical Significance - will need to split data into clinical significance and evidence status (see clinvar rating and evidence status below - if these are always the same we can get them directly from the clinvar rating and evidence status)
* Variant with equivalent alleles - e.g. rs80359585
* ClinVar rating
* Evidence status

**From the Ensembl Variant Effect Predictor**

* Allele - the variant allele used to calculate the consequence
* Gene - Ensembl stable ID of affected gene
* Feature - Ensembl stable ID of feature
* Consequence - consequence type of this variant
* Amino acid change - only given if the variant affects the protein-coding sequence
* IMPACT - the impact modifier for the consequence type
* VARIANT_CLASS - Sequence Ontology variant class
* HGVSp - the HGVS protein sequence name - especially used for searching COSMIC
* SIFT - the SIFT prediction and/or score, with both given as prediction(score) - researcher
* PolyPhen - the PolyPhen prediction and/or score - researcher
* ExAC_Adj_AF - Adjusted frequency of existing variant in ExAC combined population
* CLIN_SIG - ClinVar clinical significance of the dbSNP variant
* BIOTYPE - Biotype of transcript or regulatory feature
* APPRIS - Annotates alternatively spliced transcripts as primary or alternate based on a range of computational methods. NB: not available for GRCh37
* TSL - Transcript support level. NB: not available for GRCh37
* PUBMED - Pubmed ID(s) of publications that cite existing variant
* SOMATIC - Somatic status of existing variant(s)
* PHENO - Indicates if existing variant is associated with a phenotype, disease or trait
* GENE_PHENO - Indicates if overlapped gene is associated with a phenotype, disease or trait
* REFSEQ_MATCH - the RefSeq transcript match status; contains a number of flags indicating whether this RefSeq transcript matches the underlying reference sequence and/or an Ensembl transcript (more information). NB: not available for GRCh37.
