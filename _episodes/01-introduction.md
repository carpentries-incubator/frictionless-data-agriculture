---
title: "Introducing Frictionless Data"
teaching: 0
exercises: 0
questions:
- "What will I learn during this workshop?"
- "What are the tools that I will be using?"
- "How will learning to use Frictionless Data benefit me?"
objectives:
- "Understand the principles of Frictionless Data for tabular datasets." 
- "Understand how Frictionless Data can benefit me."
- "Have a general understanding of what Frictionless Data can do."
keypoints:
- "Frictionless can be used to create well described datasets that can be more easily re-used by other researchers."
- "Metadata is used to describe a dataset."
- "Frictionless uses a simple JSON syntax for providing structured metadata."  
---

## Motivation ##
To start, why should I use Frictionless Data for my tabular datasets? 

### What is Frictionless Data? ###
Frictionless Data is a simple open source toolkit that can be used for creating well described tabular datasets. 

Frictionless uses a suite of simple patterns to describe and organize tabular data. This allows Frictionless datasets to be shared and re-used between researchers.

Frictionless Data can also be combined with supporting Frictionless code libraries to build powerful workflows for extracting, transforming and loading data.

Frictionless uses CSV to store data. Each CSV file represents a table having columns and rows. JSON schemas are used to describe data, tables and datasets.

A Frictionless Dataset is distributed as a Frictionless Data Package. A Data Packages is composed of tabular CSV data files and a JSON metadata file. The data package can also include other files in any format such as images, PDFs, video.  

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

Frictionless allows us to capture all this information or metadata using a standard JSON metadata schema. 

## The Dataset ##

The data we will be using are based on real agricultural field experiments conducted at [Rothamsted Research](https://www.rothamsted.ac.uk/), UK. The field experiments we will be using are small plot experiments for comparing different varieties of wheat. Wheat variety is therefore our main treatment factor. The experiments are randomised with replication meaning each plot grows one variety of wheat and each variety is grown on multiple plots with varieties allocated to plots at random. 

For each plot the yield is recorded and logged to a yields.csv file. Other information for the experiment such as name, harvest area, harvest machine and varieties used is recorded in other CSV files.  

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

## Frictionless Python Module ##
The Frictionless Python module is used for creating, editing, reading and manipulating Frictionless Data. The module is split into X parts with the following uses:
1.
2.  

In the following lessons we will be using the `describe` functions to create a schema and add metadata to it.

## Goals ##
Over the following lesson episodes we will see how Frictionless Data can be used to support FAIR data, learn how Frictionless data packages are structured and describe tabular datasets and use the Frictionless python libraries to convert our three CSV files into a Frictionless Tabular Data Package.

{% include links.md %}

