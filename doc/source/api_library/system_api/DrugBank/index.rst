DrugBank System API
!!!!!!!!!!!!!!!!!!!

The DrugBank database is a unique bioinformatics and cheminformatics resource that combines detailed drug (i.e. chemical, pharmacological and pharmaceutical) data with comprehensive drug target (i.e. sequence, structure, and pathway) information. The database contains 9591 drug entries as of July 2017 including 2037 FDA-approved small molecule drugs, 241 FDA-approved biotech (protein/peptide) drugs, 96 nutraceuticals and over 6000 experimental drugs. Additionally, 4661 non-redundant protein (i.e. drug target/enzyme/transporter/carrier) sequences are linked to these drug entries. Each DrugCard entry contains more than 200 data fields with half of the information being devoted to drug/chemical data and the other half devoted to drug target or protein data.

To get an understanding of how we will use DrugBank, we can review the use via the web app (https://www.drugbank.ca). Users may query DrugBank in any number of ways. The simple text query supports general text queries of the entire textual component of the database. Clicking on the Browse button (on the DrugBank navigation panel) generates a tabular synopsis of DrugBank's content. This browse view allows users to casually scroll through the database or re-sort its contents. Clicking on a given DrugCard button brings up the full data content for the corresponding drug. A complete explanation of all the DrugCard fields and sources is given here. The PharmaBrowse button allows users to browse through drugs as grouped by their indication. This is particularly useful for pharmacists and physicians, but also for pharmaceutical researchers looking for potential drug leads. The ChemQuery button allows users to draw (using MarvinSketch applet or a ChemSketch applet) or write (SMILES string) a chemical compound and to search DrugBank for chemicals similar or identical to the query compound. The TextQuery button supports a more sophisticated text search (partial word matches, case sensitive, misspellings, etc.) of the text portion of DrugBank. The SeqSearch button allows users to conduct BLASTP (protein) sequence searches of the 18,000 sequences contained in DrugBank. Both single and multiple sequence (i.e. whole proteome) BLAST queries are supported. The Advanced Search button opens an easy-to-use relational query search tool that allows users to select or search over various combinations of subfields. The Data Extractor is the most sophisticated search tool for DrugBank. Users may download selected text components and sequence data from DrugBank and track the latest DrugBank statistics by clicking on the Download button.

A DrugBank tutorial is shown here:

https://www.youtube.com/watch?v=Le88mJ-tdb8

The DrugBank complete database and schema definition can be found here:

https://www.drugbank.ca/releases/latest

The DrugBank documentation is shown here:
https://www.drugbank.ca/documentation


**Data Inputs**
@@@@@@@@@@@@@@@


We will need to see which data are needed and build an API based on the drugbank schema through the link above or the following link:

https://www.drugbank.ca/docs/drugbank.xsd

**Required**

* Drug ID or Drug Name

**Data Outputs**
@@@@@@@@@@@@@@@@

**Step 1**
Look up rsIDs from the Defining Change(s) filed of the "Pharmacology - pharmacogenomic effects" category. The rsID will be compared with the rsIDs from the individual patient to determine if he/she has the variant of interest.

**Step 2**
If the rsID is found, retrieve the following fields from the "Pharmacology - pharmacogenomic effects" category associated with that rsID:

* Type(s): information about the pharmacogenomic effect, for example ADR = adverse drug reaction, Inferred = inferred from literature, etc.
* Description: the description of the pharmacogenomic effect
* Groups: the group the pharmacogenomic effect belongs to e.g. "slow acetylators"

Additionally, retrieve the following fields from the "Drug Identification" category:

* Groups: approved status of the drug
* Description
* Clinical Trials: necessary if the Groups statis is "investigational" or "experimental" so we should include this

Finally, retrieve the following fields from the "Interactions" category:

* Drug
* Interaction

**Additional Notes**

For full list of drugs, search for Alleles and extract Pharmacogenomic Effects/ADRs (field name). For dosing and pharmacokinetics (metabolizer status), we will need to go to Uniprot or PharmGKB.