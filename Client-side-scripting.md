Client Side Scripting:

### Using add_fetch to pull link details

    # set employee_name field to employee_name value from employee link field
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