Galaxy System API
!!!!!!!!!!!!!!!!!!!

Galaxy is an open source, web-based platform for data intensive biomedical research.

Galaxy tutorials can be found here: https://galaxyproject.org/learn/

A slide deck that gives a brief overview and walkthrough of galaxy is here: http://slideplayer.com/slide/7660335/

The figure below shows a summary of Galaxy functions:

.. image:: /_static/Galaxy-summary.png

**API Instructions Summary (tl;dr)**

These APIs will be written for a biology database called Galaxy that we have hosted on AWS. The purpose will be to import a .vcf, .bam, or .fastq files stored in S3 buckets and run the different workflows, then store the output as a file back in the same S3 bucket.

.. image:: /_static/Galaxy-process.png

Process steps:

* The API will first need to pull a .vcf file from an AWS S3 endpoint and transfer it to the AWS EC2 Galaxy endpoint. At this point no queuing is needed but we will add queuing in the future
* The API then needs to call the proper Galaxy workflows. This will annotate the file and produce a new file as an output
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

The input data should be assumed to be in a GA4GH-compatible format unless files are uploaded directly. If any new fields are added for inputs and outputs, their format should be matched as closely as possible to the GA4GH schema and they should be noted here. 

The default input format for Galaxy data is a raw file. The header information in the file will determine which workflow set it uses in Galaxy.

**Required**

* .vcf, .bam, .fa, .qv, .fastq

**Data Outputs**
@@@@@@@@@@@@@@@@

At this stage, the primary output of Galaxy after the VCFgenotypes tool will be the rsid data element. For now, the output format (JSON/XML) is unimportant. The rsid will typically be a string starting with "rs" and followed by an integer of varying length. An example is rs2383206. 

The rsids from the vcf file should be extracted and stored in the FHIR format along with the patient's data and for further processing. Any additional data we decide to store from the VCF file should be transformed into the GA4GH standard with Groovy and/or backed up as an annoted output (vcf) file in S3.

The rsids will be used in future processes to determine the health impacts of each amino acid change at each location. There might be 20,000 to millions of rsids we need to process.

**Required**

* rsid - the reference SNP ID. For example, rs2383206. These represent the location of a certain amino acid (A, C, G, or T) on a chromosome as well as the identification of that amino acid and what the change is from the reference genome.