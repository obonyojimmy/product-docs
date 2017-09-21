COSMIC System API
!!!!!!!!!!!!!!!!!!!!!

COSMIC is the most comprehensive resource for exploring the impact of somatic mutations in human cancer.

Connection instructions:
Stored here as soon as we make the docs private.

Methods and Requirements

* This must be written as a REST API
* This must follow the format and standards defined in the existing API templates located here: https://bitbucket.org/snippetmd/snippet-api-platform
* All code must be documented. We use readthedocs for our documentation, so your documentation may be in sphinx/markdown language or plain text. See more about the documentation here: http://docs.readthedocs.io/en/latest/getting_started.html


**Data Inputs**
@@@@@@@@@@@@@@@

The input data should be assumed to be in a GA4GH-compatible format unless files are uploaded directly. If any new fields are added for inputs and outputs, their format should be matched as closely as possible to the GA4GH schema and they should be noted here. 


**Required**

The input data should be assumed to be in a GA4GH-compatible format unless files are uploaded directly. If any new fields are added for inputs and outputs, their format should be matched as closely as possible to the GA4GH schema and they should be noted here.
Required

If there is an rsID, search rsID in dbSNP (e.g. rs140539427) and retrieve ideally 
#. the gene name (e.g. POLD1) from GeneView
#. protein change (e.g.  R343H)

Gene ID: To query the COSMIC database, the Ensembl Gene ID should be used. The Ensembl ID will come from the Ensembl database/API and will start with the characters “ENS” - for example, “ENSG00000139618” - a query using gene ID only (eg is BRCA2 whole gene), not for a specific variant

HUGO symbol (=gene name) & HGVS: convert Ensembl Gene ID or Entrez Gene ID to HUGO Symbol (gene name) and HGVS (only CDS and protein format) if searching for specific variants within large genes. Eg. POLD1 R343H or POLD1 c.1028G>A (gene =POLD1, variant is p.R343H for protein change, =c.1028G>A in mRNA). Note that a 1-letter amino acid code is used for COSMIC while the recommended HGVS uses the 3-letter code. 

COSMIC can be search using:

#. Gene name or HUGO synonym (eg BRAF or B-raf)
#. Tissue or cancer type such as 'lung' or 'colon' (classified in COSMIC as 'large intestine')
#. Mutation description eg the common KRAS mutation "c.35G>A" (CDS syntax) or "p.G12D" (Amino acid syntax)
#. Combined gene and mutation description eg "KRAS p.G12D"


**Data Outputs**
@@@@@@@@@@@@@@@@

**Required**

Required (when query with Gene ID or Gene Name only)
#. Overview: Drug sensitivity data - these are the drugs the mutation will be sensitive to
#. Drug resistance: This section shows the drugs that have been used to treat mutant tumours for the gene of interest. In related fields you can see any other genes that have been treated with the same drug(s), and the distribution of mutations that occur in those genes.

Required for each variant in variant table or when queried with HGVS
#. Drug resistance: same as above
#. FATHMM prediction & score: FATHMM-MKL prediction on likelihood of a variant contributing to pathogenesis of a cancer, ranging from 0-1. Scores above 0.5 are deleterious, but in order to highlight the most significant data in COSMIC, only scores ≥ 0.7 are classified as 'Pathogenic'. Mutations are classed as 'Neutral' if the score is ≤ 0.5. In addition, each functional score is classified into 10 groups of features, depending on whether it is a coding or non-coding variant. The cancer specific version of FATHMM-MKL is under development and when available these scores will be updated

From VCF file, need REF & ALT, from Ensembl VEP TXT file, need cDNA position & Gene. 
Use the Gene (= Gene accession number from Entrez - #####; and Ensembl - ENSG#####) from TXT to obtain gene name from NCBI and Ensembl. 
