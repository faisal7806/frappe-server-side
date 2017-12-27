### Table of Contents
* [UI](
* [Control](#control)

#### [Control](https://github.com/frappe/frappe/tree/develop/frappe/public/js/frappe/form/controls)
* [frappe.ui.form.ControlMultiCheck](https://github.com/frappe/frappe/blob/develop/frappe/public/js/frappe/form/controls/multicheck.js)
```js
const dialog = new frappe.ui.Dialog({
  fields: [
    {
      fieldname: 'foo', label: __('Bar'), fieldtype: 'MultiCheck',
        options: [
          { label: __('Foo'), value: 'Foo' },
          { label: __('Bar'), value: 'Bar' }
        ]
    }
  ]
});
dialog.show()
```
![](http://recordit.co/fCNz9YrxxF)
