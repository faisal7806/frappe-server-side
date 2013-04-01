Client Side Scripting:

### Make fields read-only after saving

    cur_frm.cscript.custom_refresh = function(doc) {
        // use the __islocal value of doc, to check if the doc is saved or not
        cur_frm.set_df_property("myfield", "read_only", doc.__islocal ? 0 : 1);
    }

### Hide a field based on some condition

    cur_frm.cscript.custom_refresh = function(doc) {
        cur_frm.toggle_display("myfield1", doc.myfield2=="some_value");
    }

### Get Values from Server

A standard way to query values from server side.

    wn.call({
        method:"webnotes.client.get_value",
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

    cur_frm.cscript.custom_validate = function(doc) {
        if(!doc.__islocal) {
            if(!doc.file_list) {
                var msg = wn._("Please attach atleast 1 file");
                msgprint(msg);
                throw msg;
            }
        }
    }

### Set Naming System For Item Code

    cur_frm.cscript.custom_validate = function(doc) {
        // clear item_code (name is from item_code)
        doc.item_code = "";

        // first 2 characters based on item_group
        switch(doc.item_group) {
            case "Test A":
                doc.item_code = "TA";
                break;
            case "Test B":
                doc.item_code = "TB";
                break;
            default:
                doc.item_code = "XX";
        }

        // add next 2 characters based on brand
        switch(doc.brand) {
            case "Brand A":
                doc.item_code += "BA";
                break;
            case "Brand B":
                doc.item_code += "BB";
                break;
            default:
                doc.item_code += "BX";
        }
    }

### Using add_fetch to pull link details

Add this line in the Custom Script (not in any function) for the target DocType (where you want to value to be fetched).

    // set employee_name field to employee_name value from employee link field
    // function add_fetch(link_fieldname, source_fieldname, target_fieldname)
    cur_frm.add_fetch('employee','employee_name','employee_name')

    

### Fetching Values:

Example, get default "cash_bank_account" when mode_of_payment is updated

On client side:

	cur_frm.cscript.mode_of_payment = function(doc) {
		cur_frm.call({
			method: "get_bank_cash_account",
			args: { mode_of_payment: doc.mode_of_payment }
		});
	}

On server side:

	# whitelist allows method to be called from web request
	@webnotes.whitelist()
	def get_bank_cash_account(mode_of_payment):
		return {
			"cash_bank_account": webnotes.conn.get_value("Mode of Payment", 
				mode_of_payment, "default_account")
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

on server side
```
# server script (example: in sales_invoice.py)
# not a method of DocType object of 
    
# whitelist allows method to be called from web request
@webnotes.whitelist()
def get_item_qty(item_code, wash_type):
    # do something
    fieldvalue1 = "something"

    # return a dict of row's fieldnames and values to be updated in that table row
    return { "fieldname1":  fieldvalue1 }
```

### Date Validation: Do not allow past dates in a date field

	cur_frm.cscript.custom_validate = function(doc) {
		if (doc.from_date < get_today()) {
			msgprint("You can not select past date in From Date");
			validated = false;
		}
	}

### Allow user only single perpose of stock entry:

	cur_frm.cscript.custom_validate = function(doc) {
		if(user=="user1@example.com" && doc.purpose!="Material Receipt") {
			msgprint("You are only allowed Material Receipt");
			validated = false;
		}
	}

### Validation on Stock Entry based on Warehouse Detail

	cur_frm.cscript.custom_validate = function(doc) {
		if(user_roles.indexOf("Material Manager")==-1) {
		
			var restricted_in_source = wn.model.get("Stock Entry Detail", 
				{parent:cur_frm.doc.name, s_warehouse:"Restricted"});
				
			var restricted_in_target = wn.model.get("Stock Entry Detail", 
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
		$.each(wn.model.get("Sales Team", {parent:doc.name}), function(i, d) {
    
			// calculate incentive
			var incentive_percent = 2;
			if(doc.grand_total > 400) incentive_percent = 4;

			// actual incentive
			d.incentives = flt(doc.grand_total) * incentive_percent / 100;
		});
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