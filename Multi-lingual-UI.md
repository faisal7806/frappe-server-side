## A. DocLayer

DocLayer is a pattern by which we can layer any record (doc) in the system with masks or layers. These layers will be rendered on the client side and will over-ride properties of the layers below it. This pattern will be used to implement multi-lingual views as well as customizations in DocTypes   

### Design / Implementation

#### Additional Columns
    The table will have the following columns:
    * `__lang`: Language
    * `__base`: Base record
    * `__zIndex`: A number signifying hierarchy of rendering
    
    * `__base, __lang, __zIndex` will be a unique key
    * If `__base` is null, it is the base record. It will have:
        * `__lang` = null
        * `__zIndex` = 0

#### DocLayer - serverside
   - make_layered method will add additional columns in the table to make it layerable
   - loading - load from files (if module exists), then from base sorted by zIndex  (in doc.py)
   - install_language method
      - import .txt files for that language in the db (in layerable docs), by traversing through the directory tree.
      - verify / alert if translations for any layerable doc is missing.
      - if language already installed, show confirmation box for reinstallation. If yes, first export existing translations, delete records for the particular language and then re-import from .txt files
      - provision for translation updates i.e. insert if not exists.
      - import / export provision for .xls files (since .csv doesn't support utf8)
      - uninstall a language

#### Editing
   - if layer, then show full rendered layer upto that zIndex for editing
   - on saving
      - save diff with the previous rendered layer i.e. layer flattened upto previous layer
      - save the modified time stamp of the base record only. Any change in a child record changes base record timestamp. Timestamps of child records will be null.
   - new layer, assume zIndex=(max+1)
   - validate zIndex before saving (zIndex must be unique for each language - this will be taken care of by unique index)
   - load all individual records with zIndex and render dynamically onchange of zIndex (preview functionality)

#### Rendering
   - based on `__base`, `__lang` and `__zIndex`
   - update in doclist.js (to merge dicts)
   - update sync (from server)
      - check timestamp of base record for layered tables. If required, fetch base + child records.

#### Global "Language" property
   - there will be a global default property `__lang`
   - based on `__lang`, layer will be rendered

#### UI (for editing a layered doc)
   - create new "Action", "Layers"
   - onclick, open dialog with options
      - language dropdown
      - input for zIndex

   - on save, if a record for the corresponding (language, zIndex) is not present, create it
   - a list of all layers for that doc can also be displayed (???) which on click will open that layer.

### Discussion

- If a table (say tabDoctype) contains a column 'module', search for [path to the module]/doctype/[name]/[name].txt
- If file exists, import JSON dict from the file. This will form the set of base records on which customizations, if any, will be applied in order of importance. Then apply the [name] record over the JSON dict imported from the file.
- If file doesn't exists, then the [name] record forms the base record on which customizations, if any, will be applied in order of importance.
- While applying the layers of customization, the records maybe filtered according to any criteria/column (say language), and only those records with the required criteria will be applicable as customization layers and these will be applied in order of importance. This will allow, for a start, language based DocViews. Taken further, it can be used to create highly personalized views.

## B. Messages

Make a message DocType and layer it. Messages for a particular language will have to be installed along with the `install_language` method.

- each language file for message will be a JSON object
  example: (filenames will be `<language>-<locale>.txt`)
  fr-FR.txt will contain: {'Welcome %s': 'Bienvenue %s'}
  ru-RU.txt will contain: {'Welcome %s': 'добро пожаловать %s'}

- a method `_(string)` will be used to fetch the translations for that string from tabMessage, for the language code specified in global defaults.
- we can use msgprint as msgprint(_("Welcome %s") % 'Alex') to get the translations. This is in accordance with GNU gettext.

## C. Translate

- Translating current DocTypes, Search Criteria, modules etc from Google Translate API
- Create "i18n" subfolder in the doc folder for each translated record (doc)

## D. Convert tables to utf8

Verify

## E. Internationalization

Points to consider (From Wikipedia article: http://en.wikipedia.org/wiki/Internationalization_and_localization)

- Spelling variants for different countries where the same language is spoken, e.g. localization (en-US, en-CA, en-GB-oed) vs. localisation (en-GB, en-AU)
- Plural forms in text output, which differ depending upon language
- Writing direction left to right in German, right to left in Persian, Hebrew and Arabic
- Different systems of numerals (too complex)
- Telephone numbers, addresses and international postal codes
- Currency (symbols, positions of currency markers)
- Weights and measures
- Date/time format, including use of different calendars
- Time zones (UTC in internationalized environments)
- Formatting of numbers (decimal separator, digit grouping)
- Differences in symbols (e.g. quoting text using double-quotes (" "), as in English, or guillemets (« »), as in French).
