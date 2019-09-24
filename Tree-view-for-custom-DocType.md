### This guide is obsolete as of August 2019, in favor of  the is Tree view switch in the DocType form to make any DocType a tree

<img width="1262" alt="Screenshot 2019-09-24 at 12 16 36 PM" src="https://user-images.githubusercontent.com/6195660/65488009-b64e0200-dec5-11e9-8e44-404ced1352c3.png">

***

Go through the following steps to add a tree view to any custom DocType. I'll use {{name}} as a placeholder for the `name` of the DocType, be sure to substitute your DocType's name here. I'll use account tree as an example here

## DocFields

Make sure to have the following DocFields in the custom DocType. You can add any extra fields as long as the ones below are provided

| Label           | Type  | Name            | Options  |
| --------------- | ----- | --------------- | -------- |
| Name            | Data  | {{name}}_name   |          | 
| Parent {{name}} | Link  | parent_{{name}} | {{name}} |
| Old Parent      | Link  | old_parent      | {{name}} |
| Is Group        | Check | is_group        |          |
| lft             | Int   | lft             |          |
| rgt             | Int   | rgt             |          |

### Example

![docfields_example](https://user-images.githubusercontent.com/6195660/62922736-bf798880-bdc9-11e9-8ebb-ca424ba7cf06.png)

## {{name}}.py 

You have to import NestedSet from frappe and make sure that the DocType class inherits from it

```

from frappe.util.nestedset import NestedSet

class {{name}}(NestedSet):
    nsm_parent_field = "parent_{{name}}"

```

### Example

![py_example](https://user-images.githubusercontent.com/6195660/62922971-51819100-bdca-11e9-863d-45ebf526354c.png)

## {{name}}_tree.js

You have to create this file in the same folder as the {{name}}.py file above. Make sure to assign an object to treeview_settings["{{name}}"]

```

frappe.treeview_settings["{{name}}"] = {}

```

You can use this object later to customize the tree view.

### Example

![tree_js_example](https://user-images.githubusercontent.com/6195660/62923063-8988d400-bdca-11e9-8778-58bc2e7ef187.png)


## Migrate

Run `bench migrate` for your site and you should see the tree view for the DocType.

![final](https://user-images.githubusercontent.com/6195660/62923255-fef4a480-bdca-11e9-9a8a-728ff0fba81a.png)
