	##Archived Page
###This page will no longer be maintained.  [Please see The New Wiki Page](https://github.com/frappe/erpnext/wiki/Community-Developed-Custom-Scripts) for the most up to date version.
	---

#Client Side Scripting
All client side scripting is done with javascript.
##Syntax
```
frappe.ui.form.on([DocType], {
    [trigger]: function(frm) {
        [function];
    }
});
```
Replace [DocType] with the one you want to use, in quotations.  Example:
```frappe.ui.form.on("Sales Order", {```
or
```frappe.ui.form.on("Purchase Order", {```

Replace [Trigger] with the one you want to use. Example:
```company: function(frm) {```
This would trigger the function when the company field is modified
or
```onload: function(frm) {``` This would trigger the function when the document is loaded.

List of Triggers
* Field Names (see the company example above)
* onload
* refresh
* validate
* onsubmit
* onload_post_render

Example:
```
frappe.ui.form.on("Salary Slip", {
  company: function(frm) {
    // this function is called when the value of company is changed.

  }
});
```
#Functions

## Fetching Values

[[Fetch values from another document|(Client-Side-Scripting)Fetch-values-from-another-document]]
[[Fetch a child table|(Client-Side-Scripting)Fetching-child-tables]]

## Make fields read-only after saving
```
// use the __islocal value of doc, to check if the doc is saved or not
frm.set_df_property("myfield", "read_only", frm.doc.__islocal ? 0 : 1);
```
## Hide a field based on some condition

    cur_frm.cscript.custom_refresh = function(doc) {
        cur_frm.toggle_display("myfield1", doc.myfield2=="some_value");
    }

### Get Values from Server

A standard way to query values from server side.

    frappe.call({
        method:"frappe.client.get_value",
        args: {
            doctype:"Delivery Note Item",
            filters: {
                parent:"DN00038",
                item_code:"Ser/003"
            },
            fieldname:["qty", "stock_uom"]
        }, 
        callback: function(r) { 
            console.log(r);

            // set the returned value in a field
            cur_frm.set_value(fieldname, r.message);
        }
    })

### Make attachments mandatory:
```// To be replaced ```
### Set Naming System For Item Code
```// To be replaced ```
frappe.ui.form.on("Item" {
    validate: function(frm) {
        // clear item_code
        frm.set_value("item_code","");
        if ( frm.doc.item_group === "Item Group A") {
            frm.set_value("item_code", "AA");
        } else if ( frm.doc.item_group === "Item Group B") {
            frm.set_value("item_code", "BB");
        } else {
            frm.set_value("item_group", "XX");
        if ( frm.doc.brand === "Brand 1") {
            frm.set_value("item_code", += "B1");
        } else if ( frm.doc.brand === "Brand 2") {
            frm.set_value("item_code", += "B2");
        } else {
            frm.set_value("item_code", += "B0");

### Fetching Values:
Needs Updated


Example, get default "cash_bank_account" when mode_of_payment is updated

On client side:

	cur_frm.cscript.mode_of_payment = function(doc) {
		cur_frm.call({
			method: "get_bank_cash_account",
			args: { mode_of_payment: doc.mode_of_payment }
		});
	}


### Fetching a table row's values in the form

on client side
```
// client script (example: in sales_invoice.js)
cur_frm.cscript.wash_type = function(doc, cdt, cdn) {
    var d = locals[cdt][cdn];
    if(d.wash_type) {
        cur_frm.call({
	    child: d,
	    method: "get_item_qty",
	    args: {
	        item_code: d.item_code,
	        wash_type: d.wash_type
	    }
	});
    }
}
```

### Date Validation: Do not allow past dates in a date field

	cur_frm.cscript.custom_validate = function(doc) {
		if (doc.from_date < get_today()) {
			msgprint("You can not select past date in From Date");
			validated = false;
		}
	}

### Allow user only single purpose of stock entry:

	cur_frm.cscript.custom_validate = function(doc) {
		if(user=="user1@example.com" && doc.purpose!="Material Receipt") {
			msgprint("You are only allowed Material Receipt");
			validated = false;
		}
	}

### Validation on Stock Entry based on Warehouse Detail

	cur_frm.cscript.custom_validate = function(doc) {
		if(user_roles.indexOf("Material Manager")==-1) {
		
			var restricted_in_source = frappe.model.get_list("Stock Entry Detail", 
				{parent:cur_frm.doc.name, s_warehouse:"Restricted"});
				
			var restricted_in_target = frappe.model.get_list("Stock Entry Detail", 
				{parent:cur_frm.doc.name, t_warehouse:"Restricted"})
		
			if(restricted_in_source.length || restricted_in_target.length) {
				msgprint("Only Material Manager can make entry in Restricted Warehouse");
				validated = false;
			}
		}
	}

### Calculate Incentive in Sales Team table based on some custom logic

	cur_frm.cscript.custom_validate = function(doc) {
		// calculate incentives for each person on the deal
		total_incentive = 0
		$.each(frappe.model.get_list("Sales Team", {parent:doc.name}), function(i, d) {
    
			// calculate incentive
			var incentive_percent = 2;
			if(doc.grand_total > 400) incentive_percent = 4;

			// actual incentive
			d.incentives = flt(doc.grand_total) * incentive_percent / 100;
			total_incentive += flt(d.incentives)
		});
		
		doc.total_incentive = total_incentive;
	}

### Cancel permission based on grand total

	cur_frm.cscript.custom_before_cancel = function(doc) {
		if (user_roles.indexOf("Accounts User")!=-1 && user_roles.indexOf("Accounts Manager")==-1
				&& user_roles.indexOf("System Manager")==-1) {
			if (flt(doc.grand_total) > 10000) {
				msgprint("You can not cancel this transaction, because grand total \
					is greater than 10000");
				validated = false;
			}
		}
	}

### Remove a Standard button from Form's toolbar

	cur_frm.cscript.custom_refresh = function() {
		if(!cur_frm.doc.__islocal && cur_frm.doc.owner === wn.boot.profile.name) {
			cur_frm.appframe.buttons.Submit.remove();
		}
	}

### Assign Expected Delivery Date as x days after Sales Order Date
	cur_frm.cscript.custom_sales_order_date = function(doc) {
		cur_frm.set_value("expected_delivery_date", wn.datetime.add_days(doc.sales_order_date, x));
	}

	cur_frm.cscript.custom_onload = cur_frm.cscript.custom_sales_order_date;

### Prevent back-dating for Resolution Date in Customer Issues
    if (doc.resolution_date && wn.datetime.get_day_diff(new Date(), wn.datetime.str_to_obj(doc.resolution_date)) > 0) { 
            validated = false;
             msgprint("Resolution Date cannot be a past date"); // or any other message you want..
         }

### Material Receipt in WarehouseX must be made against Material Request
	cur_frm.cscript.custom_validate = function(doc) {
		if(doc.purpose == "Material Receipt") {
			$.each(frappe.model.get("Stock Entry Detail", {parent:doc.name}), function(i, d) {
				if(d.t_warehouse=="WarehouseX" && !d.material_request) {
					msgprint("You must receive against Material Request");
					validated = false;
					return;
				}
			})
		}
	}

### Filter the selections of a field in a parent document
	cur_frm.fields_dict['item_code'].get_query = function(doc, cdt, cdn) {
		return {
			filters:{'default_supplier': doc.supplier}
		}
	}

### Filter the selections of a field in a child document
	cur_frm.fields_dict['items'].grid.get_field('item_code').get_query = function(doc, cdt, cdn) {
		return {
			filters:{'default_supplier': doc.supplier}
		}
	}