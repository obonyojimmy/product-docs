GO System API
!!!!!!!!!!!!!!!!!!!

http://www.geneontology.org/

Gene Ontology: the framework for the model of biology. The GO defines concepts/classes used to describe gene function, and relationships between these concepts. It classifies functions along three aspects:

* molecular function: molecular activities of gene products
* cellular component: where gene products are active
* biological process: pathways and larger processes made up of the activities of multiple gene products.

The Gene Ontology project provides controlled vocabularies of defined terms representing gene product properties. These cover three domains: Cellular Component, the parts of a cell or its extracellular environment; Molecular Function, the elemental activities of a gene product at the molecular level, such as binding or catalysis; and Biological Process, operations or sets of molecular events with a defined beginning and end, pertinent to the functioning of integrated living units: cells, tissues, organs, and organisms.

The GO ontology is structured as a directed acyclic graph where each term has defined relationships to one or more other terms in the same domain, and sometimes to other domains. The GO vocabulary is designed to be species-agnostic, and includes terms applicable to prokaryotes and eukaryotes, and single and multicellular organisms.

In an example of GO annotation, the gene product "cytochrome c" can be described by the Molecular Function term "oxidoreductase activity", the Biological Process terms "oxidative phosphorylation" and "induction of cell death", and the Cellular Component terms "mitochondrial matrix" and "mitochondrial inner membrane".

The figure below shows a summary of GO sources:

.. image:: /_static/GO-summary.png

**SCHEMA - DATA INPUTS AND OUTPUTS TO BE DEFINED**

Go_associations

* Association
* Association_property
* Association_qualifier
* Association_species_qualifier
* Evidence
* Evidence_dbxref
* Gene_product
* Gene_product_subset
* Gene_product_synonym
* Species

Go_audit

* Instance_data
* Source_audit
* Term_audit

Go_general

* Db
* Dbxref

Go_graph

* Relation_composition
* Relation_properties
* Term
* Term2term

Go_homology

* Gene_product_ancestor
* Gene_product_homology
* Gene_product_homolset
* Gene_product_phylotree
* Homolset
* Phylotree

Go_meta

* Term2term_metadata
* Term_dbxref
* Term_definition
* Term_subset
* Term_synonym

Go_optimisations

* Gene_product_count
* Graph_path

Go_sequence

* Gene_product_seq
* Seq
* Seq_dbxref
* Seq_property
* Public


**Data Inputs**
@@@@@@@@@@@@@@@

**Required**

* TBD

**Data Outputs**
@@@@@@@@@@@@@@@@

**Required**

* TBD

**Available but not used**

* TBD