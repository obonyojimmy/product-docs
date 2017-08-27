Ensembl System API
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

Ensembl is a genome browser for vertebrate genomes that supports research in comparative genomics, evolution, sequence variation and transcriptional regulation. Ensembl annotate genes, computes multiple alignments, predicts regulatory function and collects disease data. Ensembl tools include BLAST, BLAT, BioMart and the Variant Effect Predictor (VEP) for all supported species.

The figure below shows a summary of Ensembl functions:

.. image:: /_static/Ensembl-summary.png

**API Instructions Summary (tl;dr)**

This will be a process API for a biology database called Ensembl that we have hosted on AWS. The purpose will be to import a .vcf file stored in an S3 bucket and run the "Assembly Converter" and “Variant Effect Predictor” workflows on it, then store the output as a file back in the same S3 bucket. A high-level diagram is shown below:

.. image:: /_static/Ensembl-api-overview.png

Process steps:

* The API will first need to pull a .vcf file from an AWS S3 endpoint and transfer it to the AWS EC2 Ensembl endpoint. At this point no queuing is needed but we will add queuing in the future
* The API then needs to call the Assembly Converter followed by the Ensembl Variant Effect Predictor Workflows. This will annotate the file and produce a new file as an output
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

**Required**

We will use the output data from Galaxy as the input data for Ensembl. The Galaxy output will have two key fields that we will use as inputs:

#. Uploaded_variation : Identifier of uploaded variant. This will be an rsID if one exists, otherwise it will be a ”.” As a reminder, the rsID is the reference SNP ID. For example, e.g. rs80359585. These represent the location of a certain amino acid (A, C, G, or T) on a chromosome as well as the identification of that amino acid and what the change is from the reference genome.
#. Gene : Stable ID of affected gene. If the Galaxy Gene ID starts with "ENS" followed by a string of numbers, we will use it to query Ensembl. If the gene ID is in the NCBI format (a string of numbers only), the search will still work in Ensembl. We should pull the data to compare the output with the results from NCBI Gene (another competing standard).


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