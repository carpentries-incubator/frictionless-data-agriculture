---
title: "Frictionless Data and FAIR Data"
teaching: 0
exercises: 0
questions:
- "How does Frictionless Data relate to FAIR Data?"
objectives:
- "Understand how Frictionless Data relates to FAIR data."
keypoints:
- "Frictionless Datasets are described by metadata using a standard schema."
- "Providing good metadata to describe a dataset makes it easier for other researchers to understand and re-use the data."
- "The FAIR data principles are a set of guidelines for creating findable, accessible, interoperable and re-useable datasets."
- "Using Frictionless Data can help you create datasets that meet many of the FAIR Data Principles."
---

## What are the FAIR Data Principles ##
FAIR stands for Findable, Accessible, Interoperable and Reusable and provides an important set of guiding principles for creating reusable datasets. The FAIR data principles are being widely adopted across the research community for improving re-use of datasets

For more information on the FAIR Data Principles visit [GO-FAIR](https://www.go-fair.org/).

FAIR has 15 principles and using Frictionless we can meet 10 of them, These are:
- F1. (Meta)data are assigned a globally unique and persistent identifier
- I1. (Meta)data use a formal, accessible, shared, and broadly applicable language for knowledge representation
- I2. (Meta)data use vocabularies that follow FAIR principles
- R1. (Meta)data are richly described with a plurality of accurate and relevant attributes
- R1.1. (Meta)data are released with a clear and accessible data usage license
- R1.2. (Meta)data are associated with detailed provenance
- R1.3. (Meta)data meet domain-relevant community standards

## How does Frictionless help us meet the FAIR Data Principles ##

The Frictionless Data Package Schema provides us with a metadata schema for describing the contents and structure of a data package. The schema uses named properties such as `id`, `name`, `licences`, `sources` and `contributors` which capture specific information about a dataset. 

In the following section we will see how we can use the schema to meet specific FAIR data principles. 

### F1. (Meta)data are assigned a globally unique and persistent identifier ###

The Frictionless Data Package schema has a recommended property called `id` reserved for globally unique identifiers. An example of a globally unique identifier might be a DOI.

### I1. (Meta)data use a formal, accessible, shared, and broadly applicable language for knowledge representation. ###

The Frictionless Data Package Schema uses the JSON format to store metadata and CSV to store data. Both JSON and CSV are standard and accessible text based formats using standard formats to represent metadata and data.

### I2. (Meta)data use vocabularies that follow FAIR principles ###

Frictionless allows us to annotate data using controlled vocabularies that also follow FAIR principles. 

### R1. (Meta)data are richly described with a plurality of accurate and relevant attributes ###

It is much easier for researchers to re-use data if they can understand a dataset and make a decision whether or not it is useful for them. To help the researcher make this decision you should metadata that richly describe the data. Here plurality means including as much information as possible so that a researcher can confidently re-use the data. The Frictionless Data Package Schema provides standard metadata properties which allows us to provide rich metadata for a dataset. 

### R1.1. (Meta)data are released with a clear and accessible data usage license ###

The Frictionless Data Package Schema has a property called `licences` which allows us include a licence outlining the conditions under which the dataset can be re-used. For example a Creative Commons Attribution Licence could be applied to indicate users must credit the dataset in any publications which use it. 

### R1.2. (Meta)data are associated with detailed provenance ###

The Frictionless Data Package Schema has a property called `sources` which allows us to identify other sources of data. This can be used to show provenance of the data. We can also use other schema properties to provide text information about the provenance of the data, such as location and timing of data collection.

### R1.3. (Meta)data meet domain-relevant community standards ###

Although the Frictionless Data Package Schema defines several standard metadata properties these are very general. Frictionless allows us to add other properties for describing the dataset. For example, we could use agreed community properties such as `temporal` and `location` to describe the time and place that a dataset was generated. 

In future lessons we will see where Frictionless data is used to support these FAIR data principles.

{% include links.md %}