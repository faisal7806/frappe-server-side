## A. DocLayer

DocLayer is a pattern by which we can layer any record (doc) in the system with masks or layers. These layers will be rendered on the client side and will over-ride properties of the layers below it. This pattern will used to implement multi-lingual views as well as customizations in DocTypes   

### Design / Implementation

#### Additional Columns
    The table will have the following columns:
    * `__lang`: Language
    * `__base`: Base record
    * `__zIndex`: A number signifying hierarchy of rendering

#### DocLayer - serverside
   - make_layered method will add additional columns in the table to make it layerable
   - loading - load from files (if module exists), then from base sorted by zIndex  (in doc.py)
   - install_language method
      - import .txt files for that record and language in the db

#### Editing
   - if layer, then show full rendered layer upto that zIndex for editing
   - on saving, save diff with the previous rendered layer
   - new layer, assume zIndex=(max+1)
   - validate zIndex before saving (zIndex must be unique for each language)
   - load all individual records with zIndex and render dynamically onchange of zIndex

#### Rendering
   - based on `__base`, `__lang` and `__zIndex`
   - update in doclist.js (to merge dicts)
   - update sync (from server)

#### Global "Language" property
   - there will be a global default property `__lang`
   - based on `__lang`, layer will be rendered

#### UI (for editing a layered doc)
   - create new "Action", "Layers"
   - onclick, open dialog with options
      - language dropdown
      - input for zIndex

   - on save, if a record for the corresponding (language, zIndex) is not present, create it

### Discussion

- If a table (say tabDoctype) contains a column 'module', search for [path to the module]/doctype/[name]/[name].txt
- If file exists, import JSON dict from the file. This will form the set of base records on which customizations, if any, will be applied in order of importance. Then apply the [name] record over the JSON dict imported from the file.
- If file doesn't exists, then the [name] record forms the base record on which customizations, if any, will be applied in order of importance.
- While applying the layers of customization, the records maybe filtered according to any criteria/column (say language), and only those records with the required criteria will be applicable as customization layers and these will be applied in order of importance. This will allow, for a start, language based DocViews. Taken further, it can be used to create highly personalized views.

## B. Messages

Make a message DocType and layer it. The method `msgprint` will get the message record for that language and display it. Messages for a particular language will have to be installed along with the `install_language` method.

## C. Translate

- Translating current DocTypes, Search Criteria, modules etc from Google Translate API
- Create "i18n" subfolder in the doc folder for each translated record (doc)

## D. Convert tables to utf8

Verify