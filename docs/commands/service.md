---
hide:
- footer
---

# Service

## Description

With the service command you are able to define the state (enabled/disabled) of an installed service and set the
default version for services that support multiple parallel versions (e.g. PHP, Elasticsearch, MySQL).

The command only operates on services that are currently *[installed](install.md)* - use `install`/`uninstall`
to add or remove a service before managing its state here.

!!! Information
    All changes are "install" stable. This means "valet.sh install" will not override your state or default settings.

    To reduce the load on your system, its makes sense to stop all services you don't need!

## Overview

* *[list](service.md#list)*
* *[enable](service.md#list)*
* *[disable](service.md#list)*
* *[start](service.md#list)*
* *[stop](service.md#list)*
* *[restart](service.md#list)*
* *[default](service.md#list)*

### list

This command lists all currently *installed* services (essential and optional) in a table with the columns
`Type`, `Name`, `Default` and `Autostart`, so you can see at a glance which services are installed, which one
is the default per family (e.g. which PHP or MySQL version), and whether autostart is enabled.

```bash
valet.sh service list
```

To identify which services are currently started or stopped, you can query the underlying runtime directly. The
data services run as containers, everything else runs natively:

| Services | macOS | Ubuntu |
|----------|-------|--------|
| MySQL, MariaDB, Elasticsearch, OpenSearch, Redis, Valkey, RabbitMQ, Mailpit | `container list --all` | `podman ps` or `systemctl --user list-units 'vsh-*'` |
| PHP-FPM | `brew services list` | `systemctl status php8.3-fpm` |
| Nginx, dnsmasq | `sudo brew services list` | `systemctl status nginx` |

!!! note
    On Ubuntu the containers are started by systemd user units and are removed again when they stop, so `podman ps`
    only ever shows the services that are currently running - not even `podman ps -a` lists the stopped ones. Use
    `systemctl --user list-units 'vsh-*'` if you want to see the state of every managed service.


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

set a default version for a service. Any service that supports multiple parallel versions is "defaultable" -
that's every service configured with a `versions` array in valet.sh's bundle definitions (currently PHP, MySQL,
MariaDB, Elasticsearch, OpenSearch, Redis, Valkey and RabbitMQ).
```bash
valet.sh service default mysql80
```

* PHP: setting a default php only changes the default php on cli. You can still use any other installed PHP versions by appending the version number, e.g. "php7.0"
* Elasticsearch: the default elasticsearch is listening on port 9200. You can still use any other installed Elasticsearch version by accessing the version specific port (see *[Elasticsearch service documentation](../services/elasticsearch.md)*)
* MySQL: changes the default mysql command on cli and the version listening on port 3306. You can still access any other installed MySQL versions by appending the version number, e.g "mysql5.7", or using the version specific port (see *[MySQL service documentation](../services/mysql.md)*)


!!! warning

    Setting the default version to a disabled service will not change the state of it! You have to enable the service if you want to use it


