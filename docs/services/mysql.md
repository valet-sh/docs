---
hide:
- footer
---

# MySQL

## Version

Version 5.7, 8.0 and 8.4 of MySQL will be installed on your host. You can use each version at the same time, as different TCP ports are used.


| Type    | Version | TCP port |running by default|
|---------|---------|----------|-------|
| MySQL   | 5.7     | 3307     |YES|
| MySQL   | 8.0     | 3308     |NO|
| MySQL   | 8.4     | 3309     |NO|
| Mariadb | 10.4    | 3317     |NO|
| Mariadb | 10.6    | 3319     |NO|
| Mariadb | 11.4    | 3329     |NO|

!!! Warning
    The default MySQL can also be accessed via TCP port <string>3306</strong>!


## Manage MySQL services

Only MySQL 5.7 is running by default to reduce overall load and memory consumption. You can start/stop and enable/disable each mysql version via valet.sh.

```bash
# stop and disable MySQL 5.7
valet.sh service disable mysql57
 
# start and enable MySQL 5.7
valet.sh service enable mysql57
 
# stop and disable MySQL 8.0
valet.sh service disable mysql80
 
# start and enable MySQL 8.0
valet.sh service enable mysql80
 
# stop and disable MariaDB 10.4
valet.sh service disable mariadb104
 
# start and enable MariaDB 10.4
valet.sh service enable mariadb104

# stop and disable MariaDB 10.6
valet.sh service disable mariadb106
 
# start and enable MariaDB 10.6
valet.sh service enable mariadb106
```

!!! Warning
    You are able to start/stop a service via systemd (Ubuntu) or launchctl (macOS), but you might face some issues when running the "valet.sh install" command. 


## Access MySQL

MySQL via valet.sh only uses TCP for the connection. Unix sockets are deactivated! Instead of using "localhost" as host definition in your application, you have to use "127.0.0.1" and in most cases, when there is no separate port definition,  append the port to the host string. e.g "127.0.0.1:3306"

### Default Credentials:

| Username | Password |
|----------|----------|
| root     | root     |

!!! Warning
    Note that if you change the standard MySQL version, all configured apps with the standard port 3306 will be redirected to the new standard MySQL version. You have to create a new database, run database migrations, or export and import the db from the previous MySQL default service. You can avoid this behavior by directly using the port of the target MySQL version.


## Access MariaDB

!!! Info
    Since valet.sh 2.6.0 MariaDB is part of the MySQL service handling. Mariadb can now be set as the default "mysql" version.

### Default Credentials:

| Username | Password |
|----------|----------|
| root     | root     |

!!! Info
    Use `mariadb10.4`,`mariadump10.4` or `mariadb10.6`,`mariadump10.6` to work with MariaDB on CLI!
