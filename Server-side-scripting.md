## Warning

Custom server-side script must be consistently indented in order to function properly. This is due to Python indentation rules.

As a rule of thumb, any module-level method definition should have no indentation (i.e. not tabs before the def). For example:

    @frappe.whitelist()
    def get_some_value():
        """A module method that fetches and returns X from the database"""

Any doc-level (class-level) method definition should be properly indented (i.e. one tab before the def). For example:

        def get_some_value(self, args=None):
            """A class method that fetches and returns X from the database"""

## Examples

Coming soon...

###Querying the SQL database

To get a list of values that meet some specification from the server

    vars = frappe.db.sql("""SELECT [fieldname1], [fieldname2] 
        FROM `tab[doctype]` WHERE [fieldnameA] = %(string1)s and [fieldnameB] = %(string2)s""", 
        {'string1': input1, 'string2': input1}, as_dict=True )
    
_where:  
[fieldname1] and [fieldname2] are the fields you want returned,  
[doctype] is the document type you are querying from,  
[fieldnameA] and [fieldnameB] are the fields that filter the response based on requirements, and  
input1 and input 2 are variables determined earlier in the code._ 


The SQL queries can be used between several doctype. For example, if you wanted to find the description field of DocA that has a fieldnameB = input1 in the child table DocB, you could do the following:

    vars = frappe.db.sql("""SELECT description
        FROM `tab[docA]` as docA,`tab[docB]` as docB  WHERE docB.fieldnameB = %(string1)s and docA.name = docB.parent""", 
        {'string1': input1}, as_dict=True )

