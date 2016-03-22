# Good to know frappe functions

### frappe module

##### `frappe.form_dict`

Request parameters

##### `frappe.get_doc(doctype, name)`

e.g. frappe.get_doc('Project', 'My Project')

Load a document from the database with give doctype (table) and name
Returns a Document object. All columns are properties. e.g. doc.name

##### `frappe.get_all(doctype, filters, fields)`

e.g. frappe.get_all('Project', filters={'status': 'Open'}, fields=['name', 'description'])

Returns a list of dict objects from the database

##### `frappe.get_list(doctype, filters, fields)`

Sames as frappe.get_all, but will only show permitted for the user

##### `frappe.get_value(doctype, name, fieldname)`

Return a single value from the database 
Example: frappe.get_value('Task', 'TASK00030', 'owner')

## Document Object

##### Load a document

```
doc = frappe.get_doc(doctype, name)

# get properties
doc.title

# set properties to the document
doc.first_name = 'My Name'

# save a document to the database
doc.save()

```

### Insert a new doc

```
doc = frappe.doc({
	"doctype": "Project",
	"title": "My new project",
	"status": "Open"
})
doc.insert()
```

### How to make public API

Add `@frappe.whitelist()` to the function

Example: say your app name is `myapp`, add this to `api.py`

```
@frappe.whitelist()
def get_last_project():
	return frappe.get_all("Project", limit_page_lenght = 1)[0]
```

This will be accessible as `/api/method/myapp.api.get_last_project`

## Desk

Desk Globals:

- `cur_frm`: Current form object
- `cur_list`: Current list object 
- `cur_dialog`: Current open dialog
- `cur_page`: Current page object
- `locals`: All documents and DocType loaded in the browser session. A document can be access as `locals[doctype][name]` e.g. `locals['Opportunity']['OTY00001']`

## Forms

Form API

#### 1. To add a new handler on value change.

Example

```
frappe.ui.form.on("Salary Slip", {
  company: function(frm) {
    // this function is called when the value of company is changed.

  }
)
```

#### 2. Change value in the form

```
frm.set_value(fieldname, value);
```