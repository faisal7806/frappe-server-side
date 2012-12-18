Client Side Scripting:

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

#### Date Validation: Do not allow past dates in a date field

	cur_frm.cscript.custom_validate = function(doc) {
		if (doc.from_date < get_today()) {
			msgprint("You can not select past date in From Date");
			validated = false;
		}
	}

#### Allow user only single perpose of stock entry:

	cur_frm.cscript.custom_validate = function(doc) {
		if(user=="user1@example.com" && doc.purpose!="Material Receipt") {
			msgprint("You are only allowed Material Receipt");
			return false;
		}
	}
