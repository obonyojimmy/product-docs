NCBI Gene System API
!!!!!!!!!!!!!!!!!!!!!

The purpose of using NCBI Gene is to get the gene name from the rsID or Gene ID.

The figure below shows a summary of NCBI Gene functions:

.. image:: /_static/Galaxy-summary.png

**API Instructions Summary (tl;dr)**

Add summary here

Process steps:

#. process step 1

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

We will use the output data from Galaxy as the input data for NCBI Gene. The Galaxy output will have two key fields that we will use as inputs for NCBI Gene:

#. Uploaded_variation : Identifier of uploaded variant. This will be an rsID if one exists, otherwise it will be a ”.” As a reminder, the rsID is the reference SNP ID. For example, rs2383206. These represent the location of a certain amino acid (A, C, G, or T) on a chromosome as well as the identification of that amino acid and what the change is from the reference genome.
#. Gene : Stable ID of affected gene. If the gene ID is in the NCBI/Entrez format (a string of numbers only), you may need to add "[uid]" to the end of the string of numbers before querying. UID stands for unique record identifier. 

If the Gene ID starts with "ENS" followed by a string of numbers, this will need to be queried from the Ensembl database (Ensembl API) and should not be queried from NCBI Gene.

**Optional**

Gene name (symbol) : in the format of **Gene[sym]**_ and the term **Homo sapiens**, where offical HGNC (HUGO Gene Nomenclature Committee) name is used. Gene symbol always matches up with Gene ID but not species. Preferably use Gene ID.

**Data Outputs**
@@@@@@@@@@@@@@@@

**Required**

Phenotypes : 
-	associated conditions – list with labs that run the test (select only the ones relevant to country ie. United States. List of labs data source is NIH Genetic Testing Registry.
-	Copy number response – for only 2 triplosensitivity and haploinsufficiency from ClinGen Resource and has a score value, where 0 means no evidence and any evidence comments is available in ClinGen (can we pull the data over, link to ClinGen is on each gene record page.)


**Optional**

Interactions : interactions with other genes and description. can be a long list. Need to narrow down by options, depending on what clinician wants.

   - Expression :
   - (1) HPA RNAseq normal tissues – RNAseq normalized expression data in RPKM (reads per kilo base million) from The ‘_Human Protein Atlas project https://www.proteinatlas.org/tissue_’
   (2) Illumina BodyMap2 – RNAseq normalizsed data in RPKM in normal tissues.
 NB: RPKM will be replaced by TPM (Trancripts per million) eventually to standardize expression data across experiments.

