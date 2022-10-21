---
hide:
- footer
---

# Service

## Description

With the service command you are able to define the state (enabled/disabled) of a service and set the default version for PHP, Composer, Xdebug, Elasticsearch, and MySQL.

## Overview

* *[list](/commands/service/#list)*
* *[enable](/commands/service/#list)*
* *[disable](/commands/service/#list)*
* *[start](/commands/service/#list)*
* *[stop](/commands/service/#list)*
* *[restart](/commands/service/#list)*
* *[default](/commands/service/#list)*

### list

This command shows you the state (enabled/disabled on system startup) of each service and which one is the default.
To identify which services are currently started or stopped, you can use brew services list (macOS).

valet.sh service list
``` bash
+----------------+-------+
|    Service     | State |
+----------------+-------+
| elasticsearch1 |   0   |
+----------------+-------+
| elasticsearch2 |   0   |
+----------------+-------+
| elasticsearch5 |   0   |
+----------------+-------+
| elasticsearch6 |   1   |
+----------------+-------+
| elasticsearch7 |   0   |
+----------------+-------+
|     php56      |   0   |
+----------------+-------+
|     php70      |   0   |
+----------------+-------+
|     php71      |   0   |
+----------------+-------+
|     php72      |   1   |
+----------------+-------+
|     php73      |   1   |
+----------------+-------+
|     php74      |   1   |
+----------------+-------+
|    mysql57     |   1   |
+----------------+-------+
|    mysql80     |   0   |
+----------------+-------+
|    rabbitmq    |   0   |
+----------------+-------+
|     redis      |   1   |
+----------------+-------+
 
+-----------------+
| Default-Service |
+-----------------+
| elasticsearch6  |
+-----------------+
|     mysql57     |
+-----------------+
|      php73      |
+-----------------+
```


### enable

start the service and put in autostart
```bash
valet.sh service enable mysql80
```

### disable

stops the service and remove from autostart
```bash
valet.sh service disable mysql80
```

### start

start the service, but it will not change the behavior for autostart
```bash
valet.sh service start mysql80
```

### stop

stop the service, but it will not change the behavior for autostart
```bash
valet.sh service stop mysql80
```

### restart

restart the service, but it will not change the behavior for autostart
```bash
valet.sh service restart mysql80
```
!!! note

    Since 2.6.3 `valet.sh service restart all restarts all enabled services!

### default

set a default service. Only PHP, Elasticsearch and mysql are "defaultable" services. 
```bash
valet.sh service default mysql80
```

* PHP: setting a default php only changes the default php on cli. You can still use any other installed PHP versions by appending the version number, e.g. "php7.0"
* Elasticsearch: the default elasticsearch is listening on port 9200. You can still use any other installed Elasticsearch version by accessing the version specific port (see *[Elasticsearch service documentation](/services/elasticsearch/)*)
* MySQL: changes the default mysql command on cli and the version listening on port 3306. You can still access any other installed MySQL versions by appending the version number, e.g "mysql5.7", or using the version specific port (see *[MySQL service documentation](/services/mysql/)*)


!!! warning

    Setting the default version to a disabled service will not change the state of it! You have to enable the service if you want to use it


