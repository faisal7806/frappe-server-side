The below Client Side Script is used for calculating Number of Days between two dates.

```
frappe.ui.form.on("DOCTYPE", "refresh", function(frm, cdt, cdn) {
  var d = locals[cdt][cdn];
  frappe.model.set_value(cdt, cdn, "FIELD", frappe.datetime.get_day_diff(d.LAST_DATE, d.FIRST_DATE));
  refresh_field("FIELD");
});
```
* [DOCTYPE] Is the doctype you want the script to be executed
* [FIELD] Is the field in which you need to set the difference you get
