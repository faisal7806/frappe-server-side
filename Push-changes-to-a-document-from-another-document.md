The following code will push changes to a document.

	//Replace "DocType" with the source DocType
	frappe.ui.form.on("DocType", {
		//The trigger can be changed, but refresh must be used to use a button
		refresh: function(frm) {
			//The following line creates a button.
			frm.add_custom_button(__("Update"),
				//The function below is triggered when the button is pressed.
				function() {
					frappe.call({
						"method": "frappe.client.set_value",
						"args": {
							//replace "Target DocType" with the actual target doctype
							"doctype": "Target DocType",
							//replace target_doctype_link with a link to the document to be changed
							"name": frm.doc.target_doctype_link,
							"fieldname": {
								//You can update as many fields as you want.  
								"target_field_1": frm.doc.source_field_1,
								"target_field_2": frm.doc.source_field_2,
								"target_field_3": frm.doc.source_field_3,
								"target_field_4": frm.doc.source_field_4,
								"target_field_5": frm.doc.source_field_5  //Make sure that you do not put a comma over the last value
							},
						}
					});
			});
		}
	});

If you have any problems, please comment on the discussion thread on the ERPNext forum 
https://discuss.erpnext.com/t/tutorial-push-changes-to-another-document/18317