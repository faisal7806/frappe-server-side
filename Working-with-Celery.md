* Install and start redis

* `pip install celery redis`

* Add the following to config 
{ 
"celery_broker": "redis://localhost/", 
"celery_result_backend":null, 
"scheduler_interval": 300 
} 

* Start workers by running, 
`cd sites && python -m frappe.celery_app worker`

* beat == crontab 
`cd sites && python -m frappe.celery_app beat -s scheduler.schedule`