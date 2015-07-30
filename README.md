rdf.cdisc.org
=============

FDA/PhUSE Semantic Technology Project

Representing CDISC Foundational Standards in RDF


Introduction
------------

The FDA/PhUSE Semantic Technology project investigates how formal semantic standards can support the clinical and non-clinical trial data life cycle from protocol to submission. Within this project, several teams work on dedicated tasks to execute this investigation. The first outcome and deliverable of this project is the representation of existing CDISC standards in RDF, including representations of the following CDISC standards:

  - CDASH 1.1
  - SDTM 1.2 and SDTM Implementation Guide 3.1.2
  - SDTM 1.3 and SDTM Implementation Guide 3.1.3
  - SEND Implementation Guide 3.0
  - ADaM 2.1 and ADaM Implementation Guide 1.0
  - Controlled Terminology
  
Today, CDISC publishes these standards in a paper based format and partly in Excel, which makes it difficult to consistently represent and process this information. The RDF representation addresses both issues by providing at the same time a formal model, a machine readable representation, and an exchange format.

The main goal of this project is to represent the existing CDISC standards in RDF, not to remodel the standards, even when sometimes certain deficits became obvious. This is a conscious decision since the ownership of the standards lies within CDISC and any changes to the standards should be addressed directly by CDISC.


Distribution
------------

-- import-files --

There is an import file for each CDISC standard in RDF file. Each sheet contains a description of the instances of a single OWL class. The header of the first column is the name of OWL class. The other headers are the names of the predicates that can be applied to instances of this OWL class. Each row describes an instance. The first column contains the URI of the instance, the other columns describe the properties of the instance, which is either a literal for an owl:DatatypeProperty or a resource URI for an owl:ObjectProperty. Every resource URI is explicitly represented by its qname, we don’t assume any default namespace.


If you are new to RDF but familiar with CDISC standards, the import files should give you a very good idea of what is being represented in RDF. In that case, we would recommend to first explore the import files before turning to the RDF datasets.

-- resources --

The resources directory contains the RDF files for SKOS and Dublin Core. We use these vocabularies to annotate and document the CDISC ontologies.

-- schemas --

The schemas define the classes and predicates that constitute the ontology to represent the CDISC standards. There are three schemas. The Meta Model Schema and the CT Schema are already in use today by the NCI and are used to publish the CDISC controlled terminology in RDF. It gives a fairly compact vocabulary to represent metadata in the spirit of the ISO 11179 standard for metadata registries (MDR). The CDISC Schema defines some additional vocabulary to deal with more CDISC specific properties such as assumptions specified in the Implementation Guide, CRF completion instructions in CDASH etc.

The core element of the Metadata Model is that of an Administered Item, which may represent any item that is managed in an MDR. An administered item must be named and defined within a Context that defines the scope within which the administered item has meaning. A key administered item is that of Data Element that represents a generic unit of data. A Classifier or a defined subclass thereof offers a generic way to classify administered items. This applies in particular to data elements, e.g. an SDTM data element may be classified as Character or Numeric, or also according to compliance classifiers such as Required, Expected, or Permissible. A term of the controlled terminology of a data element is defined by a Permissible Value that is part of an Enumerated Value Domain.

Every data element belongs to a context, e.g. the data element VSTESTCD belongs to the context of the CDISC domain VS. A context can recursively be contained in a higher level context, e.g. VS belongs to the context Findings Observation Class, which in turn belongs to the context Model SDTMIG 3-1-2. One way to explore the RDF datasets is to start from a high-level context, e.g. instances of the Model class and then to follow the links to the lower level contexts.

-- terminology-2013-06-28 --

The NCI already publishes CDISC controlled terminology in RDF based on the Meta Model Schema and the CT Schema. The files included here are the ones published by the NCI in June 2013. To obtain the latest files, please follow the appropriate link from the cdisc.org web site. The files provided here are for demonstration purposes only.

-- std --

There is an RDF dataset in Turtle format (file extension ttl) for each RDF representation of a CDISC standard. There is a file all-standards that imports all the other standards, but does nothing else. This is a good starting point if you would like to explore all standards from a single entry point.


Known Issues
------------

-- File Formats --

The terminology and schema files are written in RDF/XML since this is the format the NCI currently uses. The files in this distribution are provided with both the .owl and .rdf file extensions due to requirements of some ontology editors. The CDISC standards in RDF are written in Turtle, which is a more popular format. In the future we would like to provide a distribution for both formats.

-- Meta Model Schema --

The following changes to the Meta Model Schema imply differences to the schema used by the NCI to publish the CDISC controlled terminology. It is expected that these differences will be aligned in the future.

The use of mms:broader has been replaced by the new mms:dataElement object property, which relates a Data Element Context to its Data Element. The Meta Model Schema still contains the mms:broader object property, but it is expected to be removed at a later date.

The range of mms:dataElementType has been changed from xsd:QName to xsd:string to avoid warnings from ontology editors.

The following classes have been moved from the CDISC Schema to the Meta Model Schema. This change is backward compatible for any standard importing the CDISC Schema.

  - mms:DataCollectionForm
  - mms:Domain
  - mms:DomainContext
  - mms:DataElementContext
  - mms:DataCollectionField
  - mms:Column

The ontology rdfs:label of the CT schema has been changed from "SDTM Terminology Schema" to "CDISC Terminology Schema".

-- SEND Implementation Guide --

The SEND Implementation Guide 3.0 is based on SDTM 1.2, but includes some variables that relate to the following SDTM 1.3 data elements: –ANTREG, --CSTATE, --DETECT, --DIR, --EXCLFL, --LAT, --LEAD, --PORTOT, --REASEX, --SPCUFL. No SDTM data elements were available for --ENINT, --STINT, and --METHOD (in the interventions domain).

-- Analysis Data Model --

The analysis data model has generally given more difficulties to map within the existing schemas.

Time to Event (TTE) has not been included since the documentation seems to provide only an example and is probably not to be considered a standard. Also, there are new variables in TTE that are not part of the ADaM Implementation Guide, e.g. the ASEQ variable on page 6.

The ADAE dataset is currently part of the class ADAE, but the ADAE documentation states on page 7 that the class of this dataset may change in a future version when a more general occurrence model becomes available.


Project Status
--------------

30.07.2015

The CDISC Foundational Standards in RDF haven been complemented by a Reference Guide and a User Guide. The complete package has completed CDISC Publich Review as of 30.07.2015. Currently the RDF files are available from the GitHub repository, whereas the guides can be downloaded from the CDISC web site. For more information and access to the guides, please refer to the CDISC web site http://www.cdisc.org.

30.07.2015

Work has started within CDISC to create an RDF export facility from the CDISC SHARE metadata repository. The goal is to create the CDISC Foundational Standards in RDF directly from the SHARE repository and to publish future CDISC standards in RDF as these standards become available in SHARE. As the focus now moves to a SHARE RDF export, we maintain a code freeze for the GitHub repository.


Contact
-------

For more information about the FDA/PhUSE Semantic Technology project, please visit the Wiki at phusewiki.org or go straight to phusewiki.org/wiki/index.php?title=Semantic_Technology.

