Genomic_Analysis Process API
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

**SUMMARY**

This is the main process API for analyzing genotyping tests. Individual files of different types will follow different analysis and annotation paths based on their type:

.. image:: /_static/genomic-process-api.png

**PROCESS OVERVIEW**

The universal process steps are shown below as follows:

#. Validate patient identity

#. Extract patient test data from appropriate S3 bucket using S3 api

#. Call a number of system APIs and use them to process or query the data, returning a result set

#. Store the result set in PostgreSQL and handle errors

#. Manage queuing and load balancing as needed

**VCF (FLAT FILE) PROCESS**


**BAM (SEQ) AND BED (INDEX) PROCESS**

**RAW FA AND QV PROCESS (ROCHE454)**

**RAW FASTQ PROCESS (WGS, WES)**

**RAW FASTQ PROCESS (RNAseq)**