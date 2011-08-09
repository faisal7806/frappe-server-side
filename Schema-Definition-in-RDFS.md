# Schema Definition in RDFS

All the schemas (models) will be defined in RDFS vocabulary. This will ensure standardization across
different systems and will ease of sharing data.

Also its just easier to pick someone else's hard work in defining schemas.

For all standard types, we will pick schemas from schema.org and schema.rdfs.org

## Model Files

All model files will have extension of rdfs.json and will use the json definition from rdfs.org
to define new schemas

## Persistence

There will be 3 tables

1. rdfs_Class
2. rdfs_Property
3. rdfs_Datatype

properties of these tables will be as per rdfs definitions

We will auto import all properties defined in schema.org for our easy use.


## Implementation

Will create a new module rdfs which will have methods

rdfs.sync(dict) - will update schema into the mysql table from which we can create models

## Changes to existing

1. All property definitions will use the new vocabulary
    ModelDef will become "rdfsClass"
2. In webnotes.db.table, use new DataType mapping
3. Properties can now be shared across classes
4. load_model_def will become "load_class"
5. load_class will load from database

