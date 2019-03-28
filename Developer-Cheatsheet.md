# Server Side

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

e.g. `frappe.get_all('Project', filters={'status': 'Open'}, fields=['name', 'description'])`

Returns a list of dict objects from the database

###### `frappe.get_list(doctype, filters, fields, order_by)`

Sames as frappe.get_all, but will only show records permitted for the user

Allows sorting with the order_by parameter (optional). E.g. `frappe.get_list('Payment Entry', filters={'docstatus': 0, 'payment_type': 'Pay'}, fields=['name, 'posting_date', 'paid_amount'], order_by='posting_date')`

Note that the `get_list` command will return no more than 20 items by default. To increase this, use the `limit_page_length` parameter. Using the `limit_start` parameter allows to use pagination. In case the requested is a child table, do not forget to pass the parent parameter with the parent doctype to check permissions.

###### `frappe.get_value(doctype, name, fieldname)`

Return a single value from the database 
Example: frappe.get_value('Task', 'TASK00030', 'owner')

###### `frappe.get_last_doc(doctype)`

e.g. frappe.get_last_doc('Project')

Get last created document of this type.

###### `frappe.get_single(doctype)`

e.g. frappe.get_single('Dropbox Settings')

Return a `frappe.model.document.Document` object of the given Single doctype.`

###### `frappe.get_installed_apps()`

Returns a list of all the installed apps in the current site.


## Document Object

##### Load a document

```python
doc = frappe.get_doc(doctype, name)

# get properties
doc.title

# set properties to the document
doc.first_name = 'My Name'

# save a document to the database
doc.save()

```

### Insert a new doc

```python
doc = frappe.get_doc({
	"doctype": "Project",
	"title": "My new project",
	"status": "Open"
})
doc.insert()
```

### How to make public API

Add `@frappe.whitelist()` to the function

Example: say your app name is `myapp`, add this to `api.py`

```python
@frappe.whitelist()
def get_last_project():
	return frappe.get_all("Project", limit_page_lenght = 1)[0]
```

This will be accessible as `/api/method/myapp.api.get_last_project`

### Syntax Error

You may have noticed that sometimes if there is a syntax error in your Python code and you `bench start`, it fails without telling you why.

To find out the problem, run the following commands:

```bash
cd ~/frappe-bench/sites
../env/bin/python ../apps/frappe/frappe/utils/bench_helper.py
```
Hopefully, you will get the correct traceback to fix your error.

---

# Client Side

## Desk

#### Globals

- `cur_frm`: Current form object
- `cur_list`: Current list object 
- `cur_dialog`: Current open dialog
- `cur_page`: Current page object
- `frappe.quick_entry`: Current Quick Entry object.
- `locals`: All documents and DocType loaded in the browser session. A document can be access as `locals[doctype][name]` e.g. `locals['Opportunity']['OTY00001']`

#### Routing

Routes for standard views:

- `#List/[doctype]`
- `#Form/[doctype]/[name]`
- `#Report/[doctype]`
- `#Calendar/[doctype]`
- `#modules/[module name]`

To change the route via js, use `frappe.set_route`

```js
frappe.set_route("List", "Customer");
```

##### Route Options

To pass values to a view, use global `frappe.route_options`. `frappe.route_options` is data passed to the view to whom control is being passed. For list view, it is a filter. For form, it is a default value.

Example:

```js
frappe.set_route("List", "Customer", {"customer_type": "Company"});
```

or

```js
frappe.route_options = {"customer_type": "Company"};
frappe.set_route("List", "Customer");
```

## Forms

Form API

### 1. To add a new handler on value change.
Syntax
```js
frappe.ui.form.on([DocType], {
    [trigger]: function(frm) {
        [function];
    }
});
```
Replace [DocType] with the one you want to use, in quotations.  Example:

```js
frappe.ui.form.on("Sales Order", {
```

or

```js
frappe.ui.form.on("Purchase Order", {
```
in the case of a child table, the function still calls the parent doctype.

Replace [Trigger] with the one you want to use. Example:

```js
company: function(frm) {
```

This would trigger the function when the company field is modified
or
```js
onload: function(frm) {
``` 
This would trigger the function when the document is loaded.

#### List of Triggers

* Field Names (see the company example above)
* setup
* onload
* refresh
* validate
* on_submit
* onload_post_render

What trigger is called when?

Trigger | User > Reload | `F5` | `Ctrl` + `Shift` + `R` | New Document (first time) | New Document (again) | Menu > Reload | Open document (first time) | Open document (again) | Save document
--------|---|---|---|---|---|---|---|---|---
Refresh	| ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ 
Onload	| ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ 
Setup	| ✓ | ✓ | ✓ | ✓ 

#### Child Table Triggers

Child Table Triggers need to be on the subtable DocType.

* fieldname_add
* fieldname_move
* fieldname_before_remove
* fieldname_remove

Example:

```js
frappe.ui.form.on("Salary Slip", {
  company: function(frm) {
    // this function is called when the value of company is changed.

  }
});
```

Example for child table (e.g. in Sales Invoice custom script):

```js
frappe.ui.form.on('Sales Invoice Item', {
    items_add: function(frm) {
      // adding a row ... 
   },
   items_remove: function(frm) {
      // removing a row ... 
   }
});
```

### 2. Adding Standard JS Listeners to form fields

Sometimes the built in triggers are not enough, so you can use standard JavaScript event listeners together with triggers to achieve better results. For a comprehensive list of listeners, check [this site](https://developer.mozilla.org/en-US/docs/Web/Events). The following example loads a listener once the document has been rendered and loaded. The listener runs some code when a key is pressed in the `customer` field.

```js
frappe.ui.form.on("Sales Invoice", {
    onload_post_render: function(frm) {
        // This function is run right after a Sales Invoice is rendered and loaded
        
        // This listener is added to the customer field, listening for a keypress event
        cur_frm.fields_dict.customer.$input.on("keypress", function(evt){
	    // Code specified here will run when a key is pressed on the customer field.
        });
    }
});
```

### 3. Change value in the form

```js
frm.set_value(fieldname, value);
```

### 4. Talk to the database

```js
frappe.db.get_value(doctype, filters, fieldname, callback, parent_doc)
frappe.db.get_single_value(doctype, field)
frappe.db.get_doc(doctype, name, filters = null)
frappe.db.get_list(doctype, {fields: [], limit: 20})

// check if document already exists
frappe.db.exists(doctype, name)

// insert a new document:
frappe.db.insert({
    doctype: 'Project', 
    project_name: 'Build a decent documentation', 
    expected_end_date: '2030-02-28'
})

frappe.db.delete_doc(doctype, name)
frappe.db.count(doctype, args={})
```

All are asynchronous and return a promise.

### 5. Add a new row to a child table

For example, add a new `Task` 'Update Developer Cheatsheet' to every new `Project` _on load_. (For a list of triggers, see above.)

```js
frappe.ui.form.on("Project", {
	onload: function (frm) {
		if (frm.is_new()) {
			frm.add_child('tasks').title = 'Update Developer Cheatsheet';
			frm.refresh_field('tasks');
		}
	}
});
```

* `tasks` is the name of the child table within `Project`
* we need to run `refresh_field` for the new row to become visible

## Running Tasks Serially

To run tasks serially, use `frappe.run_serially`

```js
frappe.run_serially([
  () => frappe.set_route('List', 'ToDo'),
  () => frappe.new_doc('ToDo')
]);
```

## Tests

To run individual test use 

```bash
bench --site test-service run-tests --module erpnext.tests.test_woocommerce
```

## Utility

To know list of Installed Apps of a Site
```bash
bench --site [sitename] console
frappe.get_installed_apps() 
```