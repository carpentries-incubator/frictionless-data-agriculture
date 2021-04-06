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
We are going to use Python to describe our first CSV table. 

Start Python and import the Frictionless module's `describe` function. As we'll be working with JSON and python dictionary data data structures we will also import the PrettyPrinter module to return more readable data. 

~~~
from frictionless import describe
import pprint

pp = pprint.PrettyPrinter(depth=4)
~~~
{: .language-python}

Next we'll describe the yields.csv file using the `describe` function to generate a frictionless table schema and print the results.

~~~
yields_schema = describe("data/yields.csv")
pp.pprint(schema)
~~~
{: .language-python}

This should output the following JSON table schema.

~~~
{'encoding': 'utf-8',
 'format': 'csv',
 'hashing': 'md5',
 'name': 'yields',
 'path': 'data/yields.csv',
 'profile': 'tabular-data-resource',
 'schema': {'fields': [{'name': 'plot_no', 'type': 'integer'},
                       {'name': 'expt_id', 'type': 'string'},
                       {'name': 'h_Date', 'type': 'string'},
                       {'name': 'col_y', 'type': 'integer'},
                       {'name': 'col_x', 'type': 'integer'},
                       {'name': 'variety', 'type': 'string'},
                       {'name': 'grain_weight', 'type': 'number'}]},
 'scheme': 'file'}
~~~
{: .output}

If we look at the output we can see the Frictionless `describe` function has created basic table metadata, such as the name, identified the relative location. The function has identified all the table fields and, by sampling the data rows, inferred the data type for each field.

> ## Describe the varieties and experiments files
>
> Using the code for describing the yields.csv to describe varieties.csv and experiments.csv. Assign the resulting table schemas to variables called varieties_schema and experiments_schema respectively.  
>
> > ## Solution
> > ~~~
> > varieties_schema = describe("data/varieties.csv")
> > experiments_schema = describe("data/experiments.csv")
> > ~~~
> > {: .language-python}
> > 
> {: .solution}
{: .challenge}

## Improving field descriptions

We have seen the Frictionless `describe` function generates a basic definition for each of our fields by assigning a name and data type. This is a good start for describing our tables, but it doesn't provide enough information to make the data usable. For example what are the units for grain_weight and what do col_x and row_y mean?

We can use Python to edit the table schema to improve our metadata. We will do this by adding extra field descriptors to the table schema.

### Field Descriptors

The Frictionless Table Schema uses field descriptors to provide additional information for a field. 

| Descriptor | How to use it | Example |
|------------|---------------|---------|
| name | The name *must* match a field name in the data table | hrv_date |
| title | A human readable title for the field. | Harvest date |
| description | A more detailed description of the field. | The date on which the crop was harvested. |
| type | The data type for the field. | date |
| format | The format for the field data | YYYY-MM-DD |
| rdfType | This is rich type or semantic type. It should be a URI for a term from a controlled vocabulary | http://purl.obolibrary.org/obo/TO_0000396 |
| constraints | This is used to constrain the values in a field and is used for validation | required |

Read the [Frictionless Field Descriptors documentation](https://specs.frictionlessdata.io/table-schema/#field-descriptors) for an indepth overview of the field descriptors.

### Adding field descriptors to the table schema

In python we will start adding a title and description 
~~~
yields_schema.schema.get_field("plot_no").title = "Plot Number"
yields_schema.schema.get_field("plot_no").description = "A unique identifer for the plot"

yields_schema.schema.get_field("expt_id").title = "Experiment Code"
yields_schema.schema.get_field("expt_id").description = "Institute standard code for a field experiment"

yields_schema.schema.get_field("h_date").title = "Harvest Date"
yields_schema.schema.get_field("h_date").description = "Date on which the plot was harvested"

pp.pprint(schema)
~~~
{: .language-python}

~~~
{'encoding': 'utf-8',
 'format': 'csv',
 'hashing': 'md5',
 'name': 'yields',
 'path': 'data/yields.csv',
 'profile': 'tabular-data-resource',
 'schema': {'fields': [{'description': 'A unique identifer for the plot.',
                        'name': 'plot_no',
                        'title': 'Plot Number',
                        'type': 'integer'},
                       {'description': 'Institute standard code for a field experiment.',
                        'name': 'expt_id',
                        'title': 'Experiment Code',
                        'type': 'string'},
                       {'description': 'Date on which the plot was harvested.',
                        'name': 'h_date',
                        'title': 'Harvest Date',
                        'type': 'string'},
                       {'name': 'col_y', 'type': 'integer'},
                       {'name': 'col_x', 'type': 'integer'},
                       {'name': 'variety', 'type': 'string'},
                       {'name': 'grain_weight', 'type': 'number'}]},
 'scheme': 'file'}
~~~
{: .output}

> ## Add field descriptors for the varieties and experiments tables
>
> Using the code for adding field descriptors to the yields table as an example, use the information below to add field descriptors to the varieties and experiments table schemas.  
>
> #### experiments
>
> | field name | title | description |
> |------------|-------|-------------|
> | expt_code | Experiment Code | Institute standard code for a field experiment. |
> | harvest_machine | Harvest machine | Type of machine used to harvest plots. | 
> | harvest_width | Harvest Width | Width of the area harvested in metres. |
> | harvest_length | Harvest Length | Length of the area harvested in metres. |
>  
> > ## Solution
> > ~~~
> > 
> > 
> > ~~~
> > {: .language-python}
> > 
> {: .solution}
{: .challenge}

{% include links.md %}

