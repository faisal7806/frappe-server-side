There are several helper functions built into the Frappe Framework to help with routing, creating new documents. 

`frappe.set_route()`

Used to change the route. [Example](https://github.com/frappe/erpnext/blob/096b943b0cab3807777dee933a725299fc810766/erpnext/projects/doctype/project/project.js#L58)

`frappe.route_options`

Used to pass variables to a new page. You will almost always want to end your function by emptying the variable upon completion of your method, which is usually on the destination page.[Example](https://github.com/frappe/erpnext/blob/096b943b0cab3807777dee933a725299fc810766/erpnext/projects/doctype/project/project.js#L55)


`frappe.get_route()` returns a list of the route variables

<table>
<tr><th> frappe.get_route() input </th><th> returned value </th>
<tr><td> /desk# </td><td> [""] </td></tr>
<tr><td> /desk#List/Item/List </td><td> ["List", "Item", "List"] </td></tr>
<tr><td>  /desk#Form/Stock%20Settings/Stock%20Settings </td><td> ["Form", "Stock Settings", "Stock Settings"] </td></tr>
</table>

`frappe.model.make_new_doc_and_get_name("Item");` 
Works for any (parent) doctype. [Example](https://github.com/frappe/erpnext/blob/32dc3bf0822517567acc00cf5a8924d9a1eb4ccc/erpnext/stock/doctype/stock_entry/stock_entry.js#L698)

`frappe.route.on("change", function(){`... Refactored as of 10/25/18.
[Example](https://github.com/frappe/frappe/blob/6e13fcf27f7761202e89e3acf77312832793f9b0/frappe/public/js/frappe/router_history.js#L16)