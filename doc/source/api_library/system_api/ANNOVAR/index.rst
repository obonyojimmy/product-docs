ANNOVAR System API
!!!!!!!!!!!!!!!!!!!

ANNOVAR is an efficient software tool to utilize update-to-date information to functionally annotate genetic variants detected from diverse genomes (including human genome hg18, hg19, hg38, as well as mouse, worm, fly, yeast and many others). Given a list of variants with chromosome, start position, end position, reference nucleotide and observed nucleotides, ANNOVAR can perform:

* **Gene-based annotation:** identify whether SNPs or CNVs cause protein coding changes and the amino acids that are affected. Users can flexibly use RefSeq genes, UCSC genes, ENSEMBL genes, GENCODE genes, AceView genes, or many other gene definition systems.

* **Region-based annotation:** identify variants in specific genomic regions, for example, conserved regions among 44 species, predicted transcription factor binding sites, segmental duplication regions, GWAS hits, database of genomic variants, DNAse I hypersensitivity sites, ENCODE H3K4Me1/H3K4Me3/H3K27Ac/CTCF sites, ChIP-Seq peaks, RNA-Seq peaks, or many other annotations on genomic intervals.

* **Filter-based annotation:** identify variants that are documented in specific databases, for example, whether a variant is reported in dbSNP, what is the allele frequency in the 1000 Genome Project, NHLBI-ESP 6500 exomes or Exome Aggregation Consortium, calculate the SIFT/PolyPhen/LRT/MutationTaster/MutationAssessor/FATHMM/MetaSVM/MetaLR scores, find intergenic variants with GERP++ score < 2, or many other annotations on specific mutations.
Other functionalities: Retrieve the nucleotide sequence in any user-specific genomic positions in batch, identify a candidate gene list for Mendelian diseases from exome data, and other utilities.

The figure below shows a summary of ANNOVAR annotations:

.. image:: /_static/ANNOVAR-summary.png

The API should access ANNOVAR data directly, but the web version of ANNOVAR converts a .vcf input to a .vcf tabulated output file. Here's a good article on common issues with .vcf files:

http://annovar.openbioinformatics.org/en/latest/articles/VCF/

**Data Inputs**
@@@@@@@@@@@@@@@

**Required**

* Chr
* Start
* End
* Ref
* Alt

**Data Outputs**
@@@@@@@@@@@@@@@@

We should add data structure (GA4GH / JSON / whatever) here.

**Required**

* Func.refGene
* Gene.refGene	
* GeneDetail.refGene	
* ExonicFunc.refGene	
* AAChange.refGene	
* Xref.refGene	
* cytoBand	

**Available but not used**

* SIFT_score	
* SIFT_pred
* Polyphen2_HDIV_score	
* Polyphen2_HDIV_pred	
* Polyphen2_HVAR_score	
* Polyphen2_HVAR_pred	
* LRT_score	
* LRT_pred	
* MutationTaster_score
* MutationTaster_pred	
* MutationAssessor_score	
* MutationAssessor_pred	
* FATHMM_score	
* FATHMM_pred	
* PROVEAN_score	
* PROVEAN_pred	
* VEST3_score	CADD_raw	
* CADD_phred	DANN_score	
* fathmm-MKL_coding_score	
* fathmm-MKL_coding_pred	
* MetaSVM_score	
* MetaSVM_pred	
* MetaLR_score	MetaLR_pred	
* integrated_fitCons_score	
* integrated_confidence_value	GERP++_RS	
* phyloP7way_vertebrate	
* phyloP20way_mammalian	
* phastCons7way_vertebrate	
* phastCons20way_mammalian	
* SiPhy_29way_logOdds
