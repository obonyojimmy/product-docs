PheGenI System API
!!!!!!!!!!!!!!!!!!!

The Phenotype-Genotype Integrator (PheGenI), merges NHGRI genome-wide association study (GWAS) catalog data with several databases housed at the National Center for Biotechnology Information (NCBI), including Gene, dbGaP, OMIM, GTEx and dbSNP.  This phenotype-oriented resource, intended for clinicians and epidemiologists interested in following up results from GWAS, can facilitate prioritization of variants to follow up, study design considerations, and generation of biological hypotheses.  Users can search based on chromosomal location, gene, SNP, or phenotype and view and download results including annotated tables of SNPs, genes and association results, a dynamic genomic sequence viewer, and gene expression data. PheGenI is still under active development.  Currently, the phenotype search terms are based on MeSH and will be enhanced with additional options in the future.


A video providing more information about PheGenI is available here:

https://www.youtube.com/watch?v=v_yEy--HcKc


**Data Inputs**
@@@@@@@@@@@@@@@


**Required (one of the following)**

* SNP - this is the reference SNP ID (rsID), for example rs11591147. You can try the manual search using rsid here: https://www.ncbi.nlm.nih.gov/gap/phegeni

**Optional (not currently used)**

* Location
* Gene


**Data Outputs**
@@@@@@@@@@@@@@@@


**OUTPUTS NEED TO BE SELECTED. A COMPLETE LIST IS SHOWN BELOW:**

Search Results (summary of search results - start here)

* Association Results - for example, 62 records found
* Genes - for example, 1 record found
* SNPs
* eQTL Data
* dbGaP Studies
* Genome View

Genes

* # - the search result number, for example 1
* Symbol - the gene name with link to PheGenI detailed report, for example CDKAL1 https://www.ncbi.nlm.nih.gov/gene/54901
* Description - for example, CDK5 regulatory subunit associated protein 1 like 1
* Location - for example, 6: 20,534,457 - 21,232,404
* OMIM - for example, 611259 (with link to OMIM record - https://omim.org/entry/611259)

Genome View

* Probably not applicable in most cases, presents a graphic view of the genome. May be useful in clinical research labs

Association Results

* # - the search result number, for example 1
* Trait - the phenotype trait, for example Diabetes Mellitus, Type 2. This contains a link to additional data, including “Definition” (e.g. “A subclass of diabetes mellitus that is not insulin-responsive…”), Semantic Type (e.g. “Disease or Syndrome”), Synonyms (e.g. “Adult-Onset Diabetes Mellitus, Ketosis-Resistant Diabetes…”)
* rs # - the reference SNP ID (rsid) for the gene. This also has a link to a detailed report about the SNP
* Context - the part of the DNA strand (coding or non-coding) - for example, intron or exon
* Gene - the gene name, for example CDKAL1
* Location - the gene’s location, for example 6: 20,682,391. This also has a link to a detailed report: https://www.ncbi.nlm.nih.gov/nuccore/NC_000006?report=graph&v=20682341%3A20682441&mk=20682391%7Crs35612982%7Cgreen%7C1
* P-value - the confidence level of the Genome Wide Association Study (GWAS). For example, 6X10^-36
* Source - the source for the association, for example dbGaP or NHGRI. This also has a link to the SNP or study, but seems inconsistent in where it directs the user or what data are stored. The source should be okay, but use the link at your own risk.
* Study - a study ID if available. This will also contain a link to the study if it exists. For example, phs000342 with link https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000342.v17.p10
* PubMed - a pubmed ID for the study - for example, 26818947, with link to the abstract. These would be helpful for clinicians or researchers who want to dig more into the research. Link example: https://www.ncbi.nlm.nih.gov/pubmed/26818947?dopt=Abstract

SNPs

* # - the search result number, for example 1
* Location - the gene’s location, for example 6: 20,682,391. This also has a link to a detailed report: https://www.ncbi.nlm.nih.gov/nuccore/NC_000006?report=graph&v=20682341%3A20682441&mk=20682391%7Crs35612982%7Cgreen%7C1
* Function Class - a description of the class of variant (coding, non-coding region, etc). For example, 	intron-variant, nc-transcript-variant
* Gene
* Weight
* Validation
* Diversity

eQTL Data

* #
* Tissue (Analysis ID)
* rs#
* SNP Location
* Probe ID
* Probe Location
* Gene
* P-value
* R2

dbGaP Studies

* #
* Disease - list of associated diseases based on dbGaP. For example, psoriasis, psoriatic arthritis, crohn disease
* Study Type - the type of study used to connect the gene and disease. For example, Case-Control or Nested Case-Control
* Study Name - the name of the study with a link to the study. For example, “Collaborative Association Study of Psoriasis.” Link: https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000019.v1.p1
* Participants - the number of participants in the study. For example, 2875.
* Platform - the test platform used in the study. For example, Illumina: HumanHap300v1.1




**Required**

* TBD

**Available but not used**

* TBD