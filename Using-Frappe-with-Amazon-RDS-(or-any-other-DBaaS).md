Your bench instance allows you to connect to an external database by setting a configuration in your `common_site_config.json` in your `sites` folder. 

# Setup an RDS Instance for Frappe

We're in the AWS Console, on the RDS page.

1. Click the "Create database" button.
2. Choose "Standard Create" and select "MariaDB" as the database engine.
3. Choose a supported MariaDB Version (currently, 10.3)
4. Set the "Master username" to "root" and choose a password. This is the password that bench wants to know when it asks for the "Root password".
5. Choose the size of the DB instance (at least "t2.small").
6. Optional: Enable Multi-AZ deployment for redundancy.
7. Choose the same VPC that contains your frappe server EC2 instance.
8. Select or create a parameter group that matches the below settings (for MariaDB 10.3).

```
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
default-character-set = utf8mb4
```

9. Create the database and wait until it's ready
10. Note down the "Endpoint" for that instance (for example, `instance.rds.amazonaws.com`)

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

We're on the frappe server. This should be an EC2 instance in the same VPC as the database.

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

# Move an existing database to RDS

1. Take a database backup of your site with `bench backup`.
2. Change the configuration as described in "Setup Frappe".
3. Create a **new** site and restore the backup into it.
