##Archived Page
###This page will no longer be maintained.  [Please see The New Wiki Page](https://github.com/frappe/erpnext/wiki/Community-Developed-Custom-Scripts) for the most up to date version.
---


[[This is part of a series on Client Side Scripting.  Click here to return to the Index|Client-Side-Scripting-Index]]
***

The following function allows you to pull information from another document and paste it into a field in the current one.

```
frappe.ui.form.on("[DOCTYPE]", {
	"[LINK FIELD]": function(frm) {
		frm.add_fetch("[LINK FIELD]", "[SOURCE]", "[TARGET]");
	}
});
```
* [LINK FIELD] Is a link to the document you want to fetch the information from
* [SOURCE] Is the data you are pulling from the linked document
* [TARGET] Is the field that you are placing the target into

Note:  This replaces `cur_frm.add_fetch("[LINK FIELD]", "[SOURCE]", "[TARGET]");` that is referenced in many places in the documentation and in forums.  `cur_frm` has been deprecated and should not be used.

See also: [[Fetching Child Tables|(Client-Side-Scripting)Fetching-child-tables]]

