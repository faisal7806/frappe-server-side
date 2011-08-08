### Objective

To separate .txt model files into .view and .model files. The .model files will retain the same structure, the .view files will be the form / view structure

### Structure of .view files

The view files should be read / write / parse friendly. Hence in a JSON model. Here is a sample:

	{
		'model':'Project',
		'rows': [
			{
				'heading': 'Project Details',
				'css': {
					'background-color':'BLUE'
				}
				'columns': [
					{
						'heading': 'Col 1'
						'css: {
							'width':'50%'
						},
						contents: [
							{'fieldname':'project_name', 'element':'h1', class='main-heading'},
							{'fieldname':'description'},
							{'fieldtype':'HTML', content:'<h3>hello world</h3>'}
						]
					
					},
					
					{
						{'fieldname':'project_owner'},
						{'fieldname':'start_date'},
						{'fieldname':'end_date', css: {'font-size': '22px'}},
					}
				]
				events: {
					'project_name change': function(model) {
						//do something
					}
				}
			}, 
	
			{
				'heading': 'Project To Dos',
				'columns': [
					{
						'content': [
							{'type':'list', 'list_type':'projects.todo'}
						]
					}
				]
			},
	
			{
				# column not explicitly defined
				# assume it inside the column
				'contents': [
					{'type':'list', 'list_type':'projects.project_member'}
				]
			}
		]
	}

## To Do

1. A file / db converter
2. Write the client-side form object to accept the new structure

### File Converter

1. Write .model file without 'Column Break', 'Section Break', 'HTML' fields
2. Write out .view file by breaking each section into a separate dict. Add fields in each section dict

### Form Widget

Create the following classes:
    
    class wn.widgets.Form
    class wn.widgets.FormSection
    class wn.widgets.FormField // baseclass

### Changes to doctype processing

1. Get the view file as doctype.__view and model file as doctype.__model
2. Keep individual model, view objects for each of the forms / models

API:
    
    class wn.models.Model
        get
        set
        bind    

    wn.app.models[dt][dn]
    wn.app.model_types[dt]
    
    // model attributes cannot change
    wn.app.model_attributes[dt][fieldname]
    wn.app.view_prototype[dt]
    
    // subclass this from view prototype of that class 
    wn.app.views[dt][dn] 
    wn.app.forms[dt] // all forms
    
    // switch model + get view
    wn.app.forms[dt].use[dn] 
    
## Property Separation

Properties part of model:

    fieldname
    fieldtype
    label
    reqd
    length
    index
    in_filter
    options

Properties part of view (model properties plus these):

    fieldtype (new type: HTML)
    content
    hidden
    description
    width
    height
    css
    color
