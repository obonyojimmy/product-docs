.. _apilist:


API List
!!!!!!!!!!

.. _apilist_object_ids:


System APIs
@@@@@@@@@@@

System APIs will be responsible for containing the connectors to each knowledge base or other endpoint and transoforming select data elements into a similar schema/format as GA4GH, though we will use our own data standards where it makes sense. We will not use the GA4GH API directly. 

The general format for building system APIs is as follows:

#. The API ingests data from inputs into the flow - file(s) or another API
#. After annotating the data or processing it, the flow returns the output
#. The API transforms (maps) the output data to the GA4GH or similar standardized schema
#. The API exposes the output objects or entities we need

A graphical version of the system API inputs and outputs can be seen below. 

SYSTEM API DATA FLOW INTERACTIVE DIAGRAM:

.. image:: /_static/System-api-overview.svg
            :target: ../_static/System-api-overview.svg

**Production**

**Development**

.. toctree::
   system_api/ANNOVAR/index
   system_api/Cerner_FHIR/index
   system_api/ClinVar/index
   system_api/COSMIC/index
   system_api/DrugBank/index
   system_api/EHR_FHIR/index
   system_api/Galaxy/index
   system_api/NCBI_Gene/index
   system_api/OMIM/index
   system_api/PheGenI/index

**Planned**

.. toctree::
   system_api/dbGaP/index
   system_api/dbSNP/index
   system_api/dbVar/index   
   system_api/DGVa/index
   system_api/ExAC/index
   system_api/GO/index
   system_api/MeSH/index
   system_api/RxNorm/index   


**Not Currently Planned**
.. toctree::
   system_api/ENSEMBL/index


**Templates**

.. toctree::
   system_api/EHR_FHIR/index
   system_api/Fitness_FHIR/index
   system_api/Epic_FHIR/index
   system_api/GA4GH_api/index


Process APIs
@@@@@@@@@@@@

**Production**

**Development**

**Planned**

**Templates**

.. toctree::
   process_api/Fitness_Sync/index


Experience APIs
@@@@@@@@@@@@@@@@@@@@@@

**Production**

**Development**

**Planned**

**Templates**

.. toctree::
   experience_api/Web_Portal/index


