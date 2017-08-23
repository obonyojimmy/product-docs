ExAC System API
!!!!!!!!!!!!!!!!!!!

The Exome Aggregation Consortium (ExAC) is a coalition of investigators seeking to aggregate and harmonize exome sequencing data from a variety of large-scale sequencing projects, and to make summary data available for the wider scientific community.

The data set provided in the database spans 60,706 (as of August 2017) unrelated individuals sequenced as part of various disease-specific and population genetic studies. They removed individuals affected by severe pediatric disease, so this data set should serve as a useful reference set of allele frequencies for severe disease studies. All of the raw data from these projects have been reprocessed through the same pipeline, and jointly variant-called to increase consistency across projects.

The figure below shows a summary of ExAC data:

.. image:: /_static/ExAC-summary.png

**API Instructions Summary **

TBD


Connection instructions:
Stored here as soon as we make the docs private.

Methods and Requirements

* This must be written as a REST API
* This must follow the format and standards defined in the existing API templates located here: https://bitbucket.org/snippetmd/snippet-api-platform
* All code must be documented. We use readthedocs for our documentation, so your documentation may be in sphinx/markdown language or plain text. See more about the documentation format here: http://docs.readthedocs.io/en/latest/getting_started.html


**Data Inputs**
@@@@@@@@@@@@@@@

The default input will simply be a list of reference SNP IDs (rsIDs).

**Required**

* rsid - for example, rs1800234.

**Data Outputs**
@@@@@@@@@@@@@@@@

TBD

**Required**

* TBD