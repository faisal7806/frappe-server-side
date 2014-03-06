* Install and start redis

* `pip install celery redis`

* Start workers by running, 
`cd sites && python -m frappe.celery_app worker`

* beat == crontab   
`cd sites && python -m frappe.celery_app beat -s scheduler.schedule`