In ERPNext, the data structure has many dependencies and writing a Test Case individually will require presence of all dependencies. For example testing a leave application will require the presence of a test employee record etc.

It is not feasible to write test cases for a particular database, hence there must be a system that will automatically generate all the dependant records required.

### test_runner.py

The webnotes/test_runner.py module facilitates this.

#### Get Missing Test Records

If you run the module directly via command line, and pass a DocType as an option, it will throw a list of all dependant records that are not setup and also give some more information of the DocType to help easy creation.

For example, to see if there are any dependant records for "Leave Application" to be created, from the main folder run:

    python lib/webnotes/test_runner.py "Leave Application"

This will throw out a list of any dependant records that need to be created.

#### Create Test Records

To add test records, in the python module of the DocType, just add a property test_records that will contain the list of records required for this DocType. Use the following naming convention:

1. For masters, use `_Test ` and the DocType. For example `_Test Department`
2. For naming_series, use `_T-` + DocType + `_`. For example `_T-Employee-` as the naming_series value.
3. For variants, go descriptive, example `_Test Department with Block List`

Example of test record in Employee:

	test_records = [[{
		"doctype":"Employee",
		"employee_name": "_Test Employee",
		"naming_series": "_T-Employee-",
		"date_of_joining": "2010-01-01",
		"date_of_birth": "1980-01-01",
		"gender": "Female",
		"status": "Active",
		"company": "_Test Company",
		"user_id": "test@erpnext.com"
	}]]

#### Writing the Test Case

In the test case, in the setup, just call the `webnotes.test_runner.make_test_records` method to automatically create all dependencies.

Example:

	import sys
	import unittest

	from hr.doctype.leave_application.leave_application import test_records, LeaveDayBlockedError

	class TestLeaveApplication(unittest.TestCase):
		def setUp(self):
			from webnotes.test_runner import make_test_records
			make_test_records("Leave Application")
	
		def test_block_list(self):
			import webnotes
			webnotes.conn.set_value("Employee", "_T-Employee-0001", "department", 
				"_Test Department with Block List")
			
			application = webnotes.model_wrapper(test_records[1])
			application.doc.from_date = "2013-01-01"
			application.doc.to_date = "2013-01-05"
			self.assertRaises(LeaveDayBlockedError, application.insert)
		
	if __name__=="__main__":
		sys.path.extend(["app", "lib"])
		import webnotes
		webnotes.connect()
		unittest.main()

