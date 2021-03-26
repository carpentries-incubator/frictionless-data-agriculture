---
title: "Introducing Frictionless Data"
teaching: 0
exercises: 0
questions:
- "What will I learn during this workshop?"
- "What are the tools that I will be using?"
- "How will learning to use Frictionless Data benefit me?"
objectives:
- "Understand the principles Frictionless Data for tabular datasets" 
- "Understand how Frictionless Data can benefit me."
- "Understand how Frictionless Data relates to FAIR data."
keypoints:
- "Frictionless can be used to create well described datasets."
- "Other researchers can more easily re-use well described datasets."
- "Frictionless datasets can help you to apply FAIR data principles."
- "Frictionless libraries can be used to build powerful workflows using Frictionless datasets." 
---

## Motivation ##
To start, why should I use Frictionless Data for my tabular datasets? 

### What is Frictionless Data? ###
Frictionless Data is a simple open source toolkit that can be used for creating well described tabular datasets. 

Frictionless uses a suite of simple patterns to describe and organize tabular data. This allows Frictionless datasets to be shared and re-used between researchers.

Frictionless Data can also be combined with supporting Frictionless code libraries to build powerful workflows for extracting, transforming and loading data.

Frictionless uses CSV to store data and JSON schemas to describe data and datasets.

Frictionless Data made available as a Frictionless Data Package. A Data Packages is composed of tabular CSV data files and a JSON metadata file. The data package can also include other files in in any format such as images, PDFs, video.  

### Frictionless Data is well described data ### 
> ## Why is creating well described data important?
>
> What is your experience trying to re-use datasets?    
> - Have you tried to use a dataset but puzzled over the meaning of a data column or a code for a value?
> - Was the dataset created by you or someone else?
> - Were you confident re-using these datasets, or did you abandon them?
> - Have you used datasets that you were confident using? What features of these datasets helped you to re-use them?   
{: .discussion}

Creating well described datasets makes it easier for us and others to re-use them. But what do we mean by a well described dataset?

A well described dataset means a dataset is accompanied by **metadata**. Metadata is data about the data and can include information such as:
- A data dictionary describing the tables and columns.
- A description of the dataset.
- Information about the temporal and spatial coverage of the data i.e. where and when was the data collected.
- Provenance and technical information about data collection and analysis methods used.
- Conditions for re-using the dataset such as a licence and how it should be acknowledged.
- Keywords to help dataset categorisation and discovery.
- The names of people involved in the creation of the dataset. 

Frictionless allows us to capture all this infomration or metadata using a standard JSON metadata schema. 

## Frictionless Data and FAIR Data ##
FAIR stands for Findable, Accessible, Interoperable and Reusable and provides an important set of guiding principles for creating reusable datasets.  

Using Frictionless can help you to create datasets that meet some of the key principles of the FAIR data principles. Using Frictionles can meet 10 of the 15 FAIR guiding principles. These are:
- F1. (Meta)data are assigned a globally unique and persistent identifier 
- F2. Data are described with rich metadata
- F3. Metadata clearly and explicitly include the identifier they describe
- I1. (Meta)data use a formal, accessible, shared, and broadly applicable language for knowledge representation.  
- I2. (Meta)data use vocabularies that follow FAIR principles
- I3. (Meta)data include qualified references to other (meta)data
- R1. (Meta)data are richly described with a plurality of accurate and relevant attributes
- R1.1. (Meta)data are released with a clear and accessible data usage license
- R1.2. (Meta)data are associated with detailed provenance
- R1.3. (Meta)data meet domain-relevant community standards

In future lessons we will see where Frictionless data is used to support these FAIR data principles.

## The Datasets ##

The data we will be using is a time-series from the Rothamsted Broadballk Winter Wheat long-term experiment. This is a real dataset that has been used in 100s of publications. We've simplified it for the workshop but you can download the [full dataset](http://www.era.rothamsted.ac.uk/). 

> ## Broadbalk ##
>
> The Broadbalk experiment was established in 1843 at Rothamsted, Hertforshire in the UK. It is still running today and is now officially the world's longest running agricultural experiment. The experiment is organised into plots which grow wheat either as a monocrop or in rotation with other crops. Each plot has diffetent treatments for comparing the effects of different fertilizers and of with-holding herbicides or fungicides on yield. 
{: .callout}

The datasets we'll need are:
- plots.csv
- yields.csv
- nutrients.csv

> ## Review the datasets ##
>
> Open each of these CSV files and explore them.
> - What information is stored in each file
> - Do you understand the table contents 
> - Are you confident in re-using this data
>
> What extra information could you provide to make this dataset meet FAIR data principles?
{: .discussion}

## Goals ##
Over the following lesson episodes we will document and combine the three datasets above into a Frictionless Data Package and use the Frictionless python libraries to write a pipeline for combing and transforming the data. Along the way, we will also understand how Frictionless Data can be used to support FAIR data.

{% include links.md %}

