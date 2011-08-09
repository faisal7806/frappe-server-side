# Schema Definition in RDFS

All the schemas (models) will be defined in RDFS vocabulary. This will ensure standardization across
different systems and will ease of sharing data.

Comment: All this is heavily inspired from the semantic web stuff I looked at years ago. Also its just easier to pick someone else's hard work in defining schemas. 

For all standard types, we will pick schemas from [http://schema.org](schema.org) and [http://schema.rdfs.org](rdfs.schema.org)

## Model Files

All model files will have extension of `rdfs.json` and will use the json definition from rdfs.org
to define new schemas

## Persistence

There will be a table `rdfs_triples` that will contain all the triples with subject, predicate and object

properties of these tables will be as per rdfs definitions

We will auto import all properties defined in schema.org for our easy use.

## Implementation

Will create a new module rdfs which will have methods:

    rdfs.from_json(json)
    rdfs.get_ancestors(subject)
    rdfs.get_properties(subject)
    rdfs.get_attributes(subject)

## Changes to existing

1. All property definitions will use the new vocabulary
    ModelDef will become "rdfsClass"
2. In webnotes.db.table, use new DataType mapping
3. Properties can now be shared across classes
4. load_model_def will become "load_class"
5. load_class will load from database:

### Sample Queries

    # select all attributes of a subject
    select predicate, object from rdfs_triple where subject = 'Thing'

    # get properties
    # nest this for superclass
    select subject from rdfs_triple where object in (ancestors) and predicate='domain'

### Other ideas

1. We can persist models in triples (database-triple, database-relational)
