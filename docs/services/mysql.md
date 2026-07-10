---
hide:
- footer
---

# MySQL

## Version

MySQL and MariaDB are optional and not installed by default - install the version(s) you need via
*[install](../commands/install.md)*, e.g. `valet.sh install mysql57`. You can install and run multiple versions
of each at the same time, as different TCP ports are used.

On Ubuntu, services run directly on the host and are reachable via `127.0.0.1` and their port. On macOS, services
run as Apple containers and are additionally reachable via DNS on the `vsh-services` network, using the same port.

| Type    | Version | Ubuntu           | macOS                              |
|---------|---------|------------------|--------------------------------------|
| MySQL   | 5.7     | 127.0.0.1:3307   | vsh-mysql57.vsh-services:3307        |
| MySQL   | 8.0     | 127.0.0.1:3308   | vsh-mysql80.vsh-services:3308        |
| MySQL   | 8.4     | 127.0.0.1:3309   | vsh-mysql84.vsh-services:3309        |
| MariaDB | 10.4    | 127.0.0.1:3317   | vsh-mariadb104.vsh-services:3317     |
| MariaDB | 10.6    | 127.0.0.1:3319   | vsh-mariadb106.vsh-services:3319     |
| MariaDB | 10.11   | 127.0.0.1:3324   | vsh-mariadb1011.vsh-services:3324    |
| MariaDB | 11.4    | 127.0.0.1:3329   | vsh-mariadb114.vsh-services:3329     |
| MariaDB | 11.8    | 127.0.0.1:3333   | vsh-mariadb118.vsh-services:3333     |
| MariaDB | 12.3    | 127.0.0.1:3337   | vsh-mariadb123.vsh-services:3337     |

!!! Warning
    MariaDB 10.4 is deprecated and disabled - it can no longer be installed.

!!! Warning
    The default MySQL/MariaDB is also accessed via TCP port <strong>3306</strong>!


## Manage MySQL services

Whichever version you install first becomes the default (reachable via port 3306 and the plain `mysql` CLI command)
unless you set a different one via *[service default](../commands/service.md)*. You can start/stop and enable/disable
each installed version via valet.sh.

```bash
# stop and disable MySQL 5.7
valet.sh service disable mysql57
 
# start and enable MySQL 5.7
valet.sh service enable mysql57
 
# stop and disable MySQL 8.0
valet.sh service disable mysql80
 
# start and enable MySQL 8.0
valet.sh service enable mysql80
 
# stop and disable MariaDB 10.6
valet.sh service disable mariadb106
 
# start and enable MariaDB 10.6
valet.sh service enable mariadb106
```

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
    Use `mariadb10.6`,`mariadump10.6` or `mariadb10.11`,`mariadump10.11` to work with a specific MariaDB version on CLI!
