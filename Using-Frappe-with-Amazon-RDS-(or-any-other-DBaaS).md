Your bench instance allows you to connect to an external database by setting a configuration in your `common_site_config.json` in your `sites` folder. 

**Note : if you're hosting ERPNext on an EC2 instance, use an RDS Instance on the same VPC for better performance.**

# Setup an RDS Instance for Frappe

1. Create a new database from the RDS Panel.
2. Choose "Standard Create" and select "MariaDB" as the database engine.
3. Choose a supported MariaDB Version (currently, 10.3)
4. Set the "Master username" to "root" and choose a password. This is the password that bench wants to know when it asks for the "Root password".
5. Choose the size of the DB instance (at least "t2.small").
6. Optional: Enable Multi-AZ deployment for redundancy.
7. Select or create a parameter group that matches the below settings (for MariaDB 10.3).

```
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
default-character-set = utf8mb4
```

8. Create the database and wait until it's ready
9. Note down the "Endpoint" for that instance (for example, `instance.rds.amazonaws.com`)

### Parameters for MariaDB 10.2

If you want to use MariaDB 10.2, use these parameters instead:

```
innodb-file-format = barracuda
innodb-file-per-table = 1
innodb-large-prefix = 1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
default-character-set = utf8mb4
```

# Setup Frappe

1. Test if you can connect to the database

```bash
    mysql -h instance.rds.amazonaws.com -u root -p
```

2. Open `frappe-bench/sites/common_site_config.json` with an editor

    * Add a key `db_host` and set it to the endpoint you just noted down. Add a key `rds_db` and set it to 1. The two lines should look like this:

```json
    {
        "db_host": "instance.rds.amazonaws.com",
        "rds_db": 1,
    }
```

3. Now you should be able to create a new site by running `bench new-site`

## Moving an existing database to RDS 

* Before changing the configuration you want to take a database backup of your site by doing `bench backup` 
* Once a backup is generated, change the configuration to point at RDS
* Create a **new** site and then restore the backup from the old site into it

