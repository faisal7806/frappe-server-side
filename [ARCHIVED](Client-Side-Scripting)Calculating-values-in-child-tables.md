##Archived Page
###This page will no longer be maintained.  [Please see The New Wiki Page](https://github.com/frappe/erpnext/wiki/Community-Developed-Custom-Scripts) for the most up to date version.
---

To calculate the values of child tables, you can use the following functions:
```
frappe.ui.form.on("[CHILD TABLE DOCTYPE]", {
	[CHILDTABLEMULTIPLE1]: function(frm, cdt, cdn) {
		var d = locals[cdt][cdn];
		var total = 0;
		frappe.model.set_value(d.doctype, d.name, "[CHILDTABLEPRODUCT]", d.[CHILDTABLEMULTIPLE1] * d.[CHILDTABLEMULTIPLE2]);
        frm.doc.[CHILDTABLEFIELDINPARENT].forEach(function(d) { total += d.[CHILDTABLEPRODUCT]; });
        frm.set_value('[PARENTDOCTYPETOTALFIELD]', total);
	}
});
frappe.ui.form.on("[CHILD TABLE DOCTYPE]", {
	[CHILDTABLEMULTIPLE2]: function(frm, cdt, cdn) {
		var d = locals[cdt][cdn];
		var total = 0;
		frappe.model.set_value(d.doctype, d.name, "[CHILDTABLEPRODUCT]", d.[CHILDTABLEMULTIPLE1] * d.[CHILDTABLEMULTIPLE2]);
        frm.doc.[CHILDTABLEFIELDINPARENT].forEach(function(d) { total += d.[CHILDTABLEPRODUCT]; });
        frm.set_value('[PARENTDOCTYPETOTALFIELD]', total);
	}
});
```