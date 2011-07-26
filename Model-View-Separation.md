### Objective

To separate .txt model files into .view and .model files. The .model files will retain the same structure, the .view files will be the form / view structure

### Structure of .view files

The view files should be read / write / parse friendly. Hence in a JSON model. Here is a sample:

	{
		'model':'Project',
		'sections': [
			{
				'heading': 'Project Details',
				'css': {
					'background-color':'BLUE'
				}
				'contents': [
					{'fieldname':'project_name'},
					{'fieldname':'description'},
					{'type':'html', 'content': 'Hello world'}
				],
				events: {
					'project_name change': function(model) {
						//do something
					}
				}
			}, 
	
			{
				'heading': 'Project To Dos',
				'contents': [
					{'type':'list', 'list_type':'projects.todo'}
				]
			},
	
			{
				'contents': [
					{'type':'list', 'list_type':'projects.project_member'}
				]
			}
		]
	}

### To Do

1. A file / db converter
2. Write the client-side form object to accept the new structure

### File Converter

1. Write .model file without 'Column Break', 'Section Break', 'HTML' fields
2. Write out .view file by breaking each section into a separate dict. Add fields in each section dict

### Form Widget

Create the following classes:
    
    class wn.widgets.Form
    class wn.widgets.FormSection
    class wn.widgets.FormField

### Changes to doctype processing

1. Get the view file as doctype.__view and model file as doctype.__model
2. Keep individual model, view objects for each of the forms / models

    wn.app.models[dt][dn]
    wn.app.model_types[dt]

    // model attributes cannot change
    wn.app.model_attributes[dt][fieldname]
    wn.app.view_prototype[dt]
    wn.app.views[dt][dn] // subclass this from view prototype of that class

    wn.app.forms[dt] // all forms
    wn.app.forms[dt].use[dn] // switch model + get view
    
### File structure

Move everything to js/wn folder
