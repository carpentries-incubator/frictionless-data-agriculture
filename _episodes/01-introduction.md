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

## The Dataset ##

The data we will be using is based on real agricultural field experiments conducted at [Rothamsted Research](https://www.rothamsted.ac.uk/), UK. The field experiments we will be using are small plot experiment comparing yields for different varieties of wheat. Wheat variety is therefore our main treatment factor. The experiment is randomised with replication meaning each plot grows one variety of wheat and each variety is grown on multiple plots with varieties allocated to plots at random.   

The dataset has the following three files:
1. experiment.csv
2. varieties.csv
3. yields.csv

> ## Review the datasets ##
>
> Open each of these CSV files and explore them.
> - What information is stored in each file
> - Do you understand the table contents 
> - Are you confident in re-using this data
>
> What extra information could you provide to make this dataset easier to use for other researchers?
{: .discussion}

## Goals ##
Over the following lesson episodes we will see how Frictionless Data can be used to support FAIR data, learn how Frictionless data packages are structured and describe tabular datasets and use the Frictionless python libraries to convert our three CSV files into a Frictionless Tabular Data Package.

{% include links.md %}

