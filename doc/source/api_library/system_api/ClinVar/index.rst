ClinVar System API
!!!!!!!!!!!!!!!!!!!

ClinVar is a freely accessible, public archive of reports of the relationships among human variations and phenotypes, with supporting evidence. ClinVar thus facilitates access to and communication about the relationships asserted between human variation and observed health status, and the history of that interpretation. ClinVar processes submissions reporting variants found in patient samples, assertions made regarding their clinical significance, information about the submitter, and other supporting data. The alleles described in submissions are mapped to reference sequences, and reported according to the HGVS standard. ClinVar then presents the data for interactive users as well as those wishing to use ClinVar in daily workflows and other local applications. ClinVar works in collaboration with interested organizations to meet the needs of the medical genetics community as efficiently and effectively as possible. Read more about using ClinVar.

ClinVar supports submissions of differing levels of complexity. The submission may be as simple as a representation of an allele and its interpretation (sometimes termed a variant-level submission), or as detailed as providing multiple types of structured observational (case-level) or experimental evidence about the effect of the variation on phenotype. A major goal is to support computational (re)evaluation, both of genotypes and assertions, and to enable the ongoing evolution and development of knowledge regarding variations and associated phenotypes. ClinVar is an active partner of the ClinGen project, providing data for evaluation and archiving the results of interpretation by recognized expert panels and providers of practice guidelines. ClinVar archives and versions submissions which means that when submitters update their records, the previous version is retained for review. Read more about submitting data to ClinVar.

The level of confidence in the accuracy of variation calls and assertions of clinical significance depends in large part on the supporting evidence, so this information, when available, is collected and visible to users. Because the availability of supporting evidence may vary, particularly in regard to retrospective data aggregated from published literature, the archive accepts submissions from multiple groups, and aggregates related information, to reflect transparently both consensus and conflicting assertions of clinical significance. A review status is also assigned to any assertion, to support communication about the trustworthiness of any assertion. Domain experts are encouraged to apply for recognition as an expert panel.

Accessions, of the format SCV000000000.0, are assigned to each submission. If there are multiple submissions about the same variation/condition relationship, they are aggregated within ClinVar's data flow and reported as a reference accession of the format RCV000000000.0. Because of this model, one allele will be included in multiple RCV accessions whenever different conditions are reported for that allele.

ClinVar archives submitted information, and adds identifiers and other other data that may be available about a variant or condition from other public resources. However ClinVar neither curates content nor modifies interpretations independent of an explicit submission. 

The figure below shows a summary of ClinVar data domains:

.. image:: /_static/clinvar-summary.jpg

There are also webinars and presentations with more detail here:

ftp://ftp.ncbi.nlm.nih.gov/pub/GTR/presentations/

**Data Inputs**
@@@@@@@@@@@@@@@

**POSSIBLE DATA FIELDS TO USE**

* Accession for a test registered in GTR
* AlleleID
* Base Position
* Base Position for Assembly GRCh37
* Chromosome
* ClinVar accession
* Complexity
* Creation Date
* Cytogenic band
* Disease/Phenotype
* External allele ID
* Filter
* Gene Full Name
* Gene ID
* Gene Name
* HGNC identifier for human gene
* Last interpreted
* Length of the variant
* MIM
* Modification Date
* Molecular consequence
* Name of ClinVar record
* Nucleotide/protein accession
* Organism
* Origin
* Properties
* PubMed ID
* Review Status
* Study Name
* Submitter
* Submitter Batch
* Taxonomy ID
* Text Word
* Trait Identifier
* Type of variation
* Variant name
* Variation ID


**Required**

* TBD

**Data Outputs**
@@@@@@@@@@@@@@@@

**POSSIBLE OUTPUT FIELDS TO USE**
* Variation Location - for example, GRCh37/hg19 10q23.1-25.1(chr10:85557432-105804295) GRCh37: Chr10:85557432-105804295
* Gene(s) - for example, ACTA2, FAS, ARL3, BMPR1A, ENTPD1, CHUK, ABCC2, COL17A1, COX15, CPN1, CYP2C19, CYP2C8, CYP2C9
* Condition(s) - for example, Metastatic prostate carcinoma
* Clinical significance (last reviewed) - for example, Pathogenic (Jul 23, 2015)
* Review status - for example, reviewed by expert panel
* Allele origin - for example, germline or de novo or somatic
* Method type - for example, reserach or literature only or clinical testing
* Molecular consequence - for example, frameshift or splice site or near gene
* Variation type - for example, deletion, indel, duplication
* Complexity - for example, haplotype or compound heterozygote
* Variant length - for example, less than 51 bp or between 51 and 1000 bp
* Variant-gene relationship - for example, single gene or in overlapping gene or multiple genes

**Required**

* TBD	

**Available but not used**

* TBD