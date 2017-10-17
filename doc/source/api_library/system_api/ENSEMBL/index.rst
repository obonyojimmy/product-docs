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

1. Chromosome (Galaxy ID: CHROM; Ensembl ID: chromosome) this is simply the chromosome number, represented as an integer - e.g. 1
2. Start (Galaxy ID: POS; Ensembl ID: start): this is the start position of the variant on the chromosome, and will be an integer - e.g. 881907
3. End (Galaxy ID: none - not a direct output of galaxy, this will be a calculated field; Ensembl ID: end): this is the end position of the variant on the chromosome, and will generally equal the start position with some exceptions. The logic is as follows:

Logic:
Ignore "." ("." = 0)
IF ALT = ".", "POS" + NUMBER OF CHARACTERS IN "REF" - 1 
ELSE "POS" + NUMBER OF CHARACTERS IN "ALT" - NUMBER OF CHARACTERS(A,C,G,T) IN "REF." 

Example: 
POS (start) = 56000
REF = A 
ALT = AGAT 
End = start + length(ALT) - length(REF) = 56000 + 4 - 1 = 56003

4. Allele (Galaxy ID: none - not a direct output of galaxy, this will be a calculated field; Ensembl ID: allele): This is a description of the allele, how each amino acid in the expected sequence is replaced with something else. The logic is as follows:

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

5. Strand (Galaxy ID: none, not a direct output out of galaxy; Ensembl ID = strand): this is defined as either forward (+) or reverse (-). For our purposes, Galaxy has already standardized the output for us. This value will always be "+".

We will pass the following variables into the Ensembl Variant Effect Predictor:

* chromosome (e.g. 1)
* start (e.g. 881907)
* end (e.g. 881906)
* allele (e.g. -/C)
* strand (e.g. +)

**Data Outputs**
@@@@@@@@@@@@@@@@

* Uploaded_variation: this will be the reference to tie back the variant to the input data, often the rsID e.g. rs1287637
* Consequence: the variant type e.g. splice_acceptor_variant
* Symbol: The gene symbol/name e.g. NPHP4
* Gene: The gene ID assigned by Ensembl or Entrez, e.g. ENSG0000013
* BIOTYPE: Additional information about the variant, e.g. protein_coding
* Exon: Additional information about the Exon, e.g. 15/19
* HGVSc: the HGVS or Ensembl coding ID e.g. ENST00000378156.4:c.2818-2T>A
* HGVSp: the HGVS or Ensembl protein ID e.g. ENSP00000235329.5:p.Pro559Leu
* SIFT: SIFT predicts whether an amino acid substitution is likely to affect protein function based on sequence homology and the physico-chemical similarity between the alternate amino acids. The data we provide for each amino acid substitution is a score and a qualitative prediction (either 'tolerated' or 'deleterious'). The score is the normalized probability that the amino acid change is tolerated so scores nearer 0 are more likely to be deleterious. The qualitative prediction is derived from this score such that substitutions with a score < 0.05 are called 'deleterious' and all others are called 'tolerated'. e.g. deleterious(0.04)
* PolyPhen: PolyPhen predicts the effect of an amino acid substitution on the structure and function of a protein using sequence homology, Pfam annotations, 3D structures from PDB where available, and a number of other databases and tools (including DSSP, ncoils etc.). As with SIFT, for each amino acid substitution where we have been able to calculate a prediction, we provide both a qualitative prediction (one of 'probably damaging', 'possibly damaging', 'benign' or 'unknown') and a score. The PolyPhen score represents the probability that a substitution is damaging, so values nearer 1 are more confidently predicted to be deleterious (note that this the opposite to SIFT). The qualitative prediction is based on the False Positive Rate of the classifier model used to make the predictions. e.g. benign(0.411)
* AF: Frequency of existing variant in population (note that race-specific allele frequencies exist) e.g. 0.8433
* gnomAD_AF: Frequency of existing variant in gnomAD exomes combined population e.g. 0.8277

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
