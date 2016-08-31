[[This is part of a series on Client Side Scripting.  Click here to return to the Index|Client-Side-Scripting-(new)-(wip)]]
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

Note:  This replaces `cur_frm.add_fetch("[LINK FIELD]", "[SOURCE]", "[TARGET]");` that is referenced in many places in the documentation and in forums.  `cur_frm` has been depreciated and should not be used.



