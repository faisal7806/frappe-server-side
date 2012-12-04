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

### Filtering Values in Link

