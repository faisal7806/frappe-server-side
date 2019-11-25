Your bench instance allows you to connect to an external database by setting a configuration in your `common_site_config.json` in your `sites` folder. 

**Note : It's ideal to use an RDS Instance if you're hosting your ERPNext setup on an EC2 instance on the same VPC, or else you will suffer from performance issues due to the latency.**

Here's a step-by-step tutorial on how to setup an RDS Instance for ERPNext 

* Create a MariaDB instance from the RDS Panel (Recommend at least a t2.small instance)
* Enable A-Z Deployment (this is a optional step that comes from a personal opinion)
* Make sure to keep the default username as "root"
* The password you set will be the root password
* Create a parameter group that matches the below settings : 

```
For MariaDB 10.2

innodb-file-format=barracuda
innodb-file-per-table=1
innodb-large-prefix=1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
default-character-set = utf8mb4

For MariaDB 10.3

character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
default-character-set = utf8mb4
```

* Note down the "Endpoint" for that instance
* Add a key in `common_site_config` called `db_host` and set it to the endpoint you just noted down.
* Add another key called `rds_db` and set it to 1. Your config should look something like this : 
```
  ...
  
   "update_bench_on_update": true,
   "use_tls": 1,
   "webserver_port": 8000
   "db_host": "instance.rds.amazonaws.com",
   "rds_db": 1
   }
  ```
* You should be able to now create a new site on the RDS database by doing `bench new-site` ! 

## Moving an existing database to RDS 

* Before changing the configuration you want to take a database backup of your site by doing `bench backup` 
* Once a backup is generated, change the configuration to point at RDS
* Create a **new** site and then restore the backup from the old site into it