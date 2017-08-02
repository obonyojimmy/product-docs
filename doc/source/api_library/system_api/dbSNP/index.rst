dbSNP System API
!!!!!!!!!!!!!!!!!!!

Manages information on the location and type of novel variants with causative roles in disease.

The figure below shows a summary of the dbSNP data flows:

.. image:: /_static/dbsnp-summary.png

The API should access ANNOVAR data directly, but the web version of ANNOVAR converts a .vcf input to a .vcf tabulated output file. Here's a good article on common issues with .vcf files:

http://annovar.openbioinformatics.org/en/latest/articles/VCF/

**Data Inputs**
@@@@@@@@@@@@@@@

**Required**

* chrom: the name of the chromosome (chr1, chr2, etc)
* chromStart: The reference SNP (rs) start position on the chromosome. 
* Note: the first base in a chromosome is numbered 0
* chromEnd: the rs end position on the chromosome

**Optional**

* Name: dbSNP reference name (rsID)
* Score: dbSNP does not assign a score value, so this field will always contain a 0
* Strand: this field defines strand orientation as either + or -
* There is a “BED extended format” with 30 fields, though this is being deprecated. This has been done to comply with current BED UCSC specifications - genome.ucsc.edu/faq/faqformat.html#format1. It has been tested and is compatible with the NCBI remap service, ucsc genome browser, and EBI genome browser (ensembl)


**Data Outputs**
@@@@@@@@@@@@@@@@

**Required**

* Clinical assertions (from ClinVar)
* Asserted allele origin (from ClinVar)


**Available but not used**

* Minor allele frequency
* Variation false positive status
* Others exist but we'll have to test and see what we need
