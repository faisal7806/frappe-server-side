`frappe.ui.form.on("DOCTYPE", "refresh", function(frm, cdt, cdn) {`
  `var d = locals[cdt][cdn];`
  `frappe.model.set_value(cdt, cdn, "FIELD", frappe.datetime.get_day_diff(d.LAST_DATE, d.FIRTS_DATE));`
  `refresh_field("FIELD");`
`});`