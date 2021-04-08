---
title: "Frictionless Tables"
teaching: 0
exercises: 0
questions:
- "What is a Frictionless Table Schema?"
- "How can I create and edit a Frictionless Table Schema?"
objectives:
- "Learn the Frictionless Table Schema and how it is used to describe a tabular dataset."
- "Import a table and infer metadata about it using Python."
- "Understand the Field Descriptor options for describing table fields."
- "Use Python to edit the Field Descriptors for fields in our dataset."
keypoints:
- "The Frictionless Table Schema allows us to describe metadata for a table using JSON."
- "The Frictionless python module `describe` function is used to import a file as a table and infer information about it."
- "Using the Frictionless python module we can edit the Table Schema's Field Descriptors." 
---
In this lesson we will be working with the Frictionless Python module and CSV (comma separated) data files. Each CSV file represents a table in our dataset. For each file, the first row is the header row and provides the names of the table fields. All following rows are data.

## Introducing the Frictionless Table Schema

The Frictionless Table Schema is a simple format for describing a table using JSON. The schema has properties for describing information about the table and an array property listing the tables fields. 

### Why do we need the Table Schema? ###

While CSV is a simple and effective way for providing tabular data, it only tells us the name of a field. To use the table we might need to know other information, or metadata, about the fields such as the fields data type, i.e. is it text, an integer, a decimal or a date. The Frictionless Table Schema allows us to provide this metadata for the tables fields. 

Providing additional metadata for our tables means we can improve them in three important ways:
1. We can provide validation rules for quality checking the data.
2. We can provide additional information to describe the fields and data. This makes it easier to re-use the data.
3. We can add semantic annotations to fields to improve their interoperability with other datasets.

> ## FAIR Data Principle
> 
> Providing additional metadata to describe our tables helps us to meet FAIR data principles for reuse of data.
>
{: .callout}

> ## Discussion
> 
> What other information could you provide to describe fields in a table?
>
{: .discussion}

## Describing our first table
We are going to use the Frictionless Python module to describe our first CSV table. 

Start Python or a new Jupyter Notebook and import the Frictionless module's `describe` function. As we'll be working with JSON and Python dictionary data structures we will also import the PrettyPrinter module to return more readable dictionary data. 

~~~
from frictionless import describe
import pprint

pp = pprint.PrettyPrinter(depth=4)
~~~
{: .language-python}

Next we'll describe the yields.csv file using the `describe` function to generate a Frictionless table schema and print the results.

~~~
yields_schema = describe("data/yields.csv")
pp.pprint(yields_schema)
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

If we look at the output we can see the Frictionless `describe` function has automatically *inferred* basic table and field metadata, such as the name and relative path of the file and all table fields. The `describe` function also samples the data rows to infer the data type for each field.

> ## Exercise
>
> Challenge: Describe the varieties and experiments files
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

The Frictionless Table Schema uses *Field Descriptors* to provide additional information for a field. 

| Descriptor | How to use it | Example |
|------------|---------------|---------|
| name | The name *must* match a field name in the data table | hrv_date |
| title | A human readable title for the field. | Harvest date |
| description | A more detailed description of the field. | The date on which the crop was harvested. |
| type | The data type for the field. | date |
| format | The format for the field data | YYYY-MM-DD |
| rdfType | This is rich type or semantic type. It should be a URI for a term from a controlled vocabulary | http://purl.obolibrary.org/obo/TO_0000396 |
| constraints | This is used to constrain the values in a field and is used for validation | required |

In the table schema, using the *hrv_date* field example above would give the following JSON definition:
~~~
{
    'name': 'hrv_date',
    'title': 'Harvest date',
    'description': 'The date on which the crop was harvested.',
    'type': 'date',
    'format': 'YYYY-MM-DD'
    'rdfType': 'http://purl.obolibrary.org/obo/TO_0000396',
    'constraints': {'required': True}
}
~~~
{: .source}

Read the [Frictionless Field Descriptors documentation](https://specs.frictionlessdata.io/table-schema/#field-descriptors) for an in-depth description of the field descriptors.

> ## FAIR Data Principle
> 
> Using the rdfType helps to improve interoperability of our dataset by annotating the field using a term or concept from a community vocabulary. In the above example we have used the Trait Ontology term for Harvest Date. This means we can more confidently link the data to other datasets that are similarly annotated, evern if the fields have different names. 
>
{: .callout}

### Adding field descriptors to the table schema

In python we will start adding a title and description 
~~~
yields_schema.schema.get_field("plot_no").title = "Plot Number"
yields_schema.schema.get_field("plot_no").description = "A unique identifer for the plot"

yields_schema.schema.get_field("expt_id").title = "Experiment Code"
yields_schema.schema.get_field("expt_id").description = "Institute standard code for a field experiment"

yields_schema.schema.get_field("h_date").title = "Harvest Date"
yields_schema.schema.get_field("h_date").description = "Date on which the plot was harvested"

pp.pprint(yields_schema)
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

> ## Exercise
>
> Challenge: Add field descriptors for the varieties and experiments tables
>
> Using the code for adding field descriptors to the yields table as an example, use the information below to add field descriptors to the experiments table schema.  
>
> #### experiments
>
> | field name | title | description |
> |------------|-------|-------------|
> | expt_code | Experiment Code | A unique institute standard code for a field experiment. |
> | harvest_machine | Harvest machine | Type of machine used to harvest plots. | 
> | harvest_width | Harvest Width | Width of the area harvested in metres. |
> | harvest_length | Harvest Length | Length of the area harvested in metres. |
>  
> > ## Solution
> > ~~~
> > experiments_schema.schema.get_field("expt_code").title = "Experiment Code"
> > experiments_schema.schema.get_field("expt_code").description = "A unique Institute standard code for a field experiment."
> > 
> > experiments_schema.schema.get_field("harvest_machine").title = "Harvest machine"
> > experiments_schema.schema.get_field("harvest_machine").description = "Type of machine used to harvest plots."
> > 
> > experiments_schema.schema.get_field("harvest_width").title = "Harvest Width"
> > experiments_schema.schema.get_field("harvest_width").description = "Width of the area harvested in metres."
> >
> > experiments_schema.schema.get_field("harvest_length").title = "Harvest Length"
> > experiments_schema.schema.get_field("harvest_length").description = "Length of the area harvested in metres."
> > 
> > pp.pprint(experiments_schema)
> > ~~~
> > {: .language-python}
> > 
> > ~~~
> > {
> > 'encoding': 'utf-8',
> > 'format': 'csv',
> > 'hashing': 'md5',
> > 'name': 'experiments',
> > 'path': 'data/experiments.csv',
> > 'profile': 'tabular-data-resource',
> > 'schema': {'fields': [{'description': 'A unique Institute standard code for a field experiment.',
> >                        'name': 'expt_code',
> >                        'title': 'Experiment Code',
> >                        'type': 'string'},
> >                       {'description': 'Type of machine used to harvest plots.',
> >                        'name': 'harvest_machine',
> >                        'title': 'Harvest machine',
> >                        'type': 'string'},
> >                       {'description': 'Width of the area harvested in metres.',
> >                        'name': 'harvest_width',
> >                        'title': 'Harvest Width',
> >                        'type': 'number'},
> >                       {'description': 'Length of the area harvested in metres.',
> >                        'name': 'harvest_length',
> >                        'title': 'Harvest Length',
> >                        'type': 'integer'},
> >                       {'name': 'expt_name', 
> >                        'type': 'string'},
> >                       {'name': 'site',
> >                        'type': 'string'}]},
> > 'scheme': 'file'}
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

### Adding constraint field descriptors to the table schema

We can also add constraint field descriptors to our table schema. Constraints are used to validate and quality check the data, for example, by checking numeric fields are within a certain range.

Frictionless define the following field constraints

| Constraint name | type | usage |
|-----------------|------|-------|
| required | True or False |Indicates the field __must__ have a value. |
| unique | True or False | Indicates all values in the field __must__ be unique and not repeated. |
| minLength | integer | A number indicating the minimum length for text. |
| maxLength | integer | A number indicating the maximum length for text. |
| minimum | integer | A number indicating the minimum value for a number or date. |
| maximum | integer | A number indicating the maximum value for a number or date. |
| pattern | string | A regular expression defining the format of allowed values. For example experiment codes must follow a specified institute format. |
| enum | array | A list of allowed values. All values in a field must be from this list. |

Constraint properties can be added to fields in the same way that we have just edited the title and description properties for experiments table schema. 

> ## Exercise 
> Challenge: Complete the code to add additional constraints
>
> Complete the code so that:
> 1. Experiment code is unique.  
> 2. Site must be from the list 'Brooms Barn', 'Rothamsted', 'Woburn'.
> 3. Harvest width must be between 1 and 2 m.
> 4. Harvest length must be between 1 and 10 m. 
>
> ~~~
> experiments_schema.schema.get_field("expt_code").constraints["unique"] = _________
>  
> experiments_schema.schema.get_field("site").constraints["_________"] = ["Brooms Barn","Rothamsted",_________]
> 
> experiments_schema.schema.get_field("harvest_width").constraints["minimum"] = _________
> experiments_schema.schema.get_field("harvest_width").constraints[""] = 2
> 
> _________.schema.get_field(_________).constraints[_________] = _________
> _________.schema.get_field(_________).constraints[_________] = _________
> 
> pp.pprint(_________)
> ~~~
> {: .language-python}
>  
> > ## Solution
> > ~~~
> > experiments_schema.schema.get_field("expt_code").constraints["unique"] = True
> >  
> > experiments_schema.schema.get_field("site").constraints["enum"] = ["Brooms Barn","Rothamsted","Woburn"]
> >
> > experiments_schema.schema.get_field("harvest_width").constraints["minimum"] = 1
> > experiments_schema.schema.get_field("harvest_width").constraints["maximum"] = 2
> >
> > experiments_schema.schema.get_field("harvest_length").constraints["minimum"] = 1
> > experiments_schema.schema.get_field("harvest_length").constraints["maximum"] = 10
> > 
> > pp.pprint(experiments_schema)
> > ~~~
> > {: .language-python}
> > 
> > ~~~
> > {
> > 'encoding': 'utf-8',
> > 'format': 'csv',
> > 'hashing': 'md5',
> > 'name': 'experiments',
> > 'path': 'data/experiments.csv',
> > 'profile': 'tabular-data-resource',
> > 'schema': {'fields': [{'constraints': {'unique': True},
> >                        'description': 'A unique Institute standard code for a field experiment.',
> >                        'name': 'expt_code',
> >                        'title': 'Experiment Code',
> >                        'type': 'string'},
> >                       {'description': 'Type of machine used to harvest plots.',
> >                        'name': 'harvest_machine',
> >                        'title': 'Harvest machine',
> >                        'type': 'string'},
> >                       {'constraints': {'maximum': 2, 'minimum': 1},
> >                        'description': 'Width of the area harvested in metres.',
> >                        'name': 'harvest_width',
> >                        'title': 'Harvest Width',
> >                        'type': 'number'},
> >                       {'constraints': {'maximum': 10, 'minimum': 1},
> >                        'description': 'Length of the area harvested in metres.',
> >                        'name': 'harvest_length',
> >                        'title': 'Harvest Length',
> >                        'type': 'integer'},
> >                       {'name': 'expt_name', 'type': 'string'},
> >                       {'constraints': {'enum': ['Brooms Barn',
> >                                                 'Rothamsted',
> >                                                 'Woburn']},
> >                        'name': 'site',
> >                        'type': 'string'}]},
> > 'scheme': 'file'}
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

{% include links.md %}

