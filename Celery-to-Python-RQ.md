If your Frappé app had a background job defined using a decorator `@celery_task()` in `yourapp/tasks.py` like [this](https://github.com/frappe/erpnext/blob/76568f0e8e194c2a3ed692ce46ea75a27a100929/erpnext/tasks.py#L10), then you need to modify the function definition and its queuing as follows:

### Using Celery (before):

In `yourapp/tasks.py`:

```
@celery_task()
def do_something(site, param1, param2, ...):
    try:
        frappe.connect(site=site) # or frappe.init(site)
        ...

    except:
        frappe.db.rollback()
        ...

    else:
        frappe.db.commit()

    finally:
        frappe.destroy()

```

and its call somewhere (like [this](https://github.com/frappe/erpnext/blob/76568f0e8e194c2a3ed692ce46ea75a27a100929/erpnext/crm/doctype/newsletter/newsletter.py#L39)):

```
from yourapp.tasks import do_something
...

def some_method():
    ...
    do_something.delay(frappe.local.site, param1=param1, param2=param2, ...)

```

### Using Python RQ (after):

In `yourapp/tasks.py`:

```
# No need for the site parameter. This function is called after init and connect!

def do_something(param1, param2, ...):
    try:
        ...

    except:
        frappe.db.rollback()
        ...

    else:
        frappe.db.commit()

    # no need to call frappe.destroy() in finally, as this is handled by frappe

```


and its call somewhere

```
from yourapp.tasks import do_something
from frappe.utils.background_jobs import enqueue
...

def some_method():
    ...
    enqueue(do_something, param1=param1, param2=param2, ...)

```

Also, it is not required for you to keep the `do_something` method in `yourapp/tasks.py` anymore. You can keep it in any importable file and import it at the top.

You can also pass `timeout` in seconds to `enqueue`