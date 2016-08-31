The following function will allow you to copy the values from a child table and paste them into another.

```
frappe.ui.form.on("[TARGETDOCTYPE]", {
    "[TRIGGER]": function(frm) {
        frappe.model.with_doc("[SOURCEDOCTYPE]", frm.doc.[TRIGGER], function() {
            var tabletransfer= frappe.model.get_doc("[SOURCEDOCTYPE]", frm.doc.[TRIGGER])
            $.each(tabletransfer.[SOURCECHILDTABLE], function(index, row){
                d = frm.add_child("[TARGETCHILDTABLE]");
                d.[TARGETFIELD1] = row.[SOURCEFIELD1];
                d.[TARGETFIELD2] = row.[SOURCEFIELD2];
                frm.refresh_field("[TARGETCHILDTABLE]");
            });
        });
    }
});

```
* [TARGETDOCTYPE] - The doctype that is being worked in.
    * [TARGETCHILDTABLE] - The table to be populated.  This value is the name of the table field in the parent doctype.
        *[TARGETFIELD] - The field name in the target child table.
* [SOURCEDOCTYPE] - The doctype that contains the information to be pulled
    * [SOURCECHILDTABLE] - The table to pull information from.  This value is the name of the table field in the parent doctype.
        *[SOURCEFIELD] - The field name to pull data from within the table.
* [TRIGGER] - What causes the function to activate.