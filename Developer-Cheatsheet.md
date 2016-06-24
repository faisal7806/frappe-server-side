# Good to know frappe functions

### frappe module

###### `frappe.form_dict`

Request parameters

###### `frappe.get_doc(doctype, name)`

e.g. frappe.get_doc('Project', 'My Project')

Load a document from the database with give doctype (table) and name
Returns a Document object. All columns are properties. e.g. doc.name

###### `frappe.get_meta(doctype)`

Loads the metadata (DocType) of the given doctype.

e.g. `frappe.get_meta('Task').fields` is the list of fields in Task doctype

###### `frappe.get_all(doctype, filters, fields)`

e.g. frappe.get_all('Project', filters={'status': 'Open'}, fields=['name', 'description'])

Returns a list of dict objects from the database

###### `frappe.get_list(doctype, filters, fields)`

Sames as frappe.get_all, but will only show permitted for the user

###### `frappe.get_value(doctype, name, fieldname)`

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

#### Globals

- `cur_frm`: Current form object
- `cur_list`: Current list object 
- `cur_dialog`: Current open dialog
- `cur_page`: Current page object
- `locals`: All documents and DocType loaded in the browser session. A document can be access as `locals[doctype][name]` e.g. `locals['Opportunity']['OTY00001']`

#### Routing

Routes for standard views:

- `#List/[doctype]`
- `#Form/[doctype]/[name]`
- `#Report/[doctype]`
- `#Calendar/[doctype]`
- `#modules/[module name]`

To change the route via js, use `frappe.set_route`

```
frappe.set_route("List", "Customer");
```

##### Route Options

To pass values to a view, use global `frappe.route_options`. `frappe.route_options` is data passed to the view to whom control is being passed. For list view, it is a filter. For form, it is a default value.

Example:

```
frappe.set_route("List", "Customer", {"customer_type": "Company"});
```

or

```
frappe.route_options = {"customer_type": "Company"};
frappe.set_route("List", "Customer");
```

## Forms

Form API

#### 1. To add a new handler on value change.
Syntax
```
frappe.ui.form.on([DocType], {
    [trigger]: function(frm) {
        [function];
    }
});
```
Replace [DocType] with the one you want to use, in quotations.  Example:
```frappe.ui.form.on("Sales Order", {```
or
```frappe.ui.form.on("Purchase Order", {```
in the case of a child table, the function still calls the parent doctype.

Replace [Trigger] with the one you want to use. Example:
```company: function(frm) {```
This would trigger the function when the company field is modified
or
```onload: function(frm) {``` This would trigger the function when the document is loaded.

List of Triggers
* Field Names (see the company example above)
* onload
* refresh
* validate
* onsubmit

Example:
```
frappe.ui.form.on("Salary Slip", {
  company: function(frm) {
    // this function is called when the value of company is changed.

  }
});
```

#### 2. Change value in the form

```
frm.set_value(fieldname, value);
```