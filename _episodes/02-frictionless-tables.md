---
title: "Frictionless Tables"
teaching: 0
exercises: 0
questions:
- "What is a Frictionless Table Schema?"
- "How can I create a Frictionless Table Schema?"
- "What can I do with a Frictionless table?"
objectives:
- "Learn the Frictionless Table Schema and how it is used to describe a tabular dataset."
- "Import a table and infer metadata about."
- "Edit table metadata."
- "Add additional column properties."
- "Identify primary key columns."
- "Add a foreign key to create a relationship with another tables."
- "Validate a tables data"

keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
## Introducing the Frictionless Table Schema

The Frictionless Table Schema is a simple format for describing a table and is expressed as JSON.

The schema describes the properties of a tabular dataset. Tabular data consists of a set of rows and a set of fields (columns). In this lesson we will be working with CSV (comma separated) formatted files. In these files, the first row is the header row and provides the names of the tables fields.

While CSV is a simple way of formatting tabular data, it only tells us the name of a field. To use the table we might need to know other information, or metadata, about the fields such as the fields data type. The Frictionless Table Schema allows us to provide this field metadata.

> ## Describing tabular data fields
>
> What other information could you provide to describe fields in a table?
>
{: .discussion}

## Describing our first table
We are going to use Python to describe our first CSV table




### Field Descriptors

The Frictionless Table Schema uses field descriptors to provide additional information for a field. 

| Descriptor | How to use it | Example |
|------------|---------------|---------|
| name | The name *must* match a field name in the data table | hrv_date |
| title | A human readable title for the field. | Harvest date |
| description | A more detailed description of the field. | The date on which the crop was harvested. |
| type | The data type for the field. | date |
| format | The format for the field data | YYYY-MM-DD |
| rdfType | This is rich type or semantic type. It should be a URI for a term from a controlled vocabulary | |
| constraints | This is used to constrain the values in a field and is used for validation | required |

Read the [Frictionless Field Descriptors documentation](https://specs.frictionlessdata.io/table-schema/#field-descriptors) for an indepth overview of the field descriptors.







{% include links.md %}

