---
hide:
- footer
---

# Upgrade from valet.sh 2.x to 3.x

!!! warning
    valet.sh 3.x is still under active development - this page and the rest of the 3.x documentation may change
    without notice. Use the version selector above to switch back to the current stable 2.x documentation.

!!! danger "No data is migrated"
    valet.sh 3.x runs all data services in containers, and those containers start with **empty** volumes. Your
    databases, search indexes, caches and message queues from 2.x are **not** taken over.

    Create a backup of everything you still need **before** you switch - see *[Back up your data](#2-back-up-your-data)*.

!!! danger "Intel Macs must stay on valet.sh 2.x"
    valet.sh 3.x only supports Apple Silicon. If you are on an Intel Mac, do **not** switch the release channel -
    there is no upgrade path and no 3.x support for your machine. See *[Support-Matrix](support-matrix.md)*.

## What changes in 3.x

| Topic | valet.sh 2.x | valet.sh 3.x |
|-------|--------------|--------------|
| Data services | native packages (Homebrew / apt) | containers |
| Container runtime | - | Apple Containers (macOS), Podman + systemd user units (Ubuntu) |
| Scope of an installation | everything is pre-installed | only `nginx`, `dnsmasq` and `mailpit`; everything else on demand |
| Removing a service | not possible | *[uninstall](../commands/uninstall.md)* |
| Where data is stored | directories on your host | container volumes (`vsh-<service>-data`) |
| Your existing data | - | not migrated |
| Operating systems | Intel + Apple Silicon, older releases | Apple Silicon only, macOS 26+, Ubuntu 24.04 / 26.04 |
| Mail catcher | Mailhog | *[Mailpit](../services/mailpit.md)* (`mailpit.test`) |
| MariaDB 10.4 | available | deprecated and disabled |
| RabbitMQ web interface | `rabbitmq.test` | one host per version, e.g. `rabbitmq313.test` |

### Data services now run in containers

MySQL, MariaDB, Elasticsearch, OpenSearch, Redis, Valkey, RabbitMQ and Mailpit no longer run as native packages on
your machine. They run as containers - managed by valet.sh, so you keep using the same
*[service](../commands/service.md)* commands to start, stop, enable or disable them.

PHP (including PHP-FPM), Nginx, dnsmasq, Composer, Node.js and Magerun still run natively and are not affected by
this change.

### Nothing is installed by default anymore

A 3.x installation only provides the essential baseline (`nginx`, `dnsmasq`, `mailpit`). Every other service is
optional and has to be installed explicitly via *[install](../commands/install.md)*, or automatically by
*[init-instance](../commands/init-instance.md)* based on your project's
*[.valet-sh.yml](../how-to-articles/project-configuration-via-valet-sh-yml.md)*.

This means that right after the upgrade **no database, no search engine, no cache and no PHP version is available**
until you install it. Write down what you are using now, before you start - see
*[Take stock of your setup](#1-take-stock-of-your-current-setup)*.

### Data lives in container volumes

Each containerized service keeps its data in a named volume, e.g. `vsh-mysql80-data` for MySQL 8.0. Re-running
`valet.sh install mysql80` re-applies the provisioning (for example an updated configuration file) and **keeps your
data**. Your data is only deleted if you explicitly ask for it by uninstalling a service with `--purge`.

### How services are reached

On **Ubuntu** the containers use the host network, so everything stays reachable at `127.0.0.1` and the same ports
as in 2.x - no changes to your project configuration are needed.

On **macOS** each container gets its own IP address and a DNS name in the `.vsh` domain. Only the *default* database
(port 3306) and the *default* search engine (port 9200) are additionally proxied to `127.0.0.1`, as in 2.x.
Every other version is reachable via its container name only:

| Service | Ubuntu | macOS |
|---------|--------|-------|
| default database | 127.0.0.1:3306 | 127.0.0.1:3306 |
| default search engine | 127.0.0.1:9200 | 127.0.0.1:9200 |
| MySQL 5.7 | 127.0.0.1:3307 | vsh-mysql57.vsh:3307 |
| MySQL 8.0 | 127.0.0.1:3308 | vsh-mysql80.vsh:3308 |
| Elasticsearch 7 | 127.0.0.1:9207 | vsh-elasticsearch7.vsh:9207 |
| Redis 6 | 127.0.0.1:6379 | vsh-redis6.vsh:6379 |
| RabbitMQ 3.13 (AMQP) | 127.0.0.1:5674 | vsh-rabbitmq313.vsh:5674 |

If you are on macOS and your projects address a version-specific port on `127.0.0.1` (e.g. `127.0.0.1:3308`), you
have to *[update your project configuration](#6-update-your-project-configuration-macos-only)* after the upgrade.
The command line clients (`mysql8.0`, `mysqldump8.0`, ...) work unchanged on both operating systems.

## Upgrade at a glance

1. *[Take stock of your current setup](#1-take-stock-of-your-current-setup)*
2. *[Back up your data](#2-back-up-your-data)*
3. *[Switch to the 3.x release channel](#3-switch-to-the-3x-release-channel)*
4. *[Install the services you need](#4-install-the-services-you-need)*
5. *[Restore your data](#5-restore-your-data)*
6. *[Update your project configuration (macOS only)](#6-update-your-project-configuration-macos-only)*

Please read all instructions carefully and run command by command. If you run into any errors, please report them
before continuing, to ensure the issue gets fixed for the next person to upgrade.

## 1. Take stock of your current setup

3.x will not install anything for you automatically, so note down which services, versions and projects you are
actually using while you are still on 2.x:

```bash
# all services, their state and which version is the default per family
valet.sh service list

# all linked projects and their PHP versions
valet.sh links

# all databases of the default database service
valet.sh db ls
```

!!! note
    Keep this list. You will need it in *[step 4](#4-install-the-services-you-need)* to install the same set of
    services again.

## 2. Back up your data

All commands in this section are executed **while you are still on 2.x**. Store your backups outside of
`/usr/local/valet-sh`, for example in `~/valet-sh-2x-backup`:

```bash
mkdir -p ~/valet-sh-2x-backup
```

### MySQL and MariaDB

Every database you still need must be exported. Keep in mind that a dump only ever covers **one** service version -
if you use several versions in parallel, repeat the export for each of them.

| Type | Version | Port | Client / dump command |
|---------|---------|------|--------------------------|
| MySQL | 5.7 | 3307 | `mysql5.7` / `mysqldump5.7` |
| MySQL | 8.0 | 3308 | `mysql8.0` / `mysqldump8.0` |
| MySQL | 8.4 | 3309 | `mysql8.4` / `mysqldump8.4` |
| MariaDB | 10.4 | 3317 | `mariadb10.4` / `mariadump10.4` |
| MariaDB | 10.6 | 3319 | `mariadb10.6` / `mariadump10.6` |
| MariaDB | 10.11 | 3324 | `mariadb10.11` / `mariadump10.11` |
| MariaDB | 11.4 | 3329 | `mariadb11.4` / `mariadump11.4` |

The quickest way for a single database on the **default** database service:

```bash
cd ~/valet-sh-2x-backup

# creates ~/valet-sh-2x-backup/projectx-2x.sql.gz
valet.sh db export projectx-2x projectx
```

!!! note
    *[valet.sh db](../commands/db.md)* always writes into the current directory and always appends `.sql.gz`, and it
    only talks to the **default** database service. For every other version, use the version-specific dump command
    below.

To export **all** databases of one specific version - here MySQL 8.0 on port 3308 - into one file per database:

```bash
for db in $(mysql8.0 -h127.0.0.1 -P3308 -uroot -proot -N -B -e "SHOW DATABASES" \
    | grep -Ev '^(information_schema|performance_schema|mysql|sys)$'); do
  echo "dumping ${db}"
  mysqldump8.0 -h127.0.0.1 -P3308 -uroot -proot \
    --single-transaction --no-tablespaces --routines --events --triggers \
    "${db}" | gzip > ~/valet-sh-2x-backup/mysql80-"${db}".sql.gz
done
```

The internal schemas (`information_schema`, `performance_schema`, `mysql`, `sys`) are skipped on purpose - they must
not be restored into a fresh 3.x service. For MariaDB, use the matching client and port, e.g.
`mariadump10.6 -h127.0.0.1 -P3319 ...`.

!!! warning
    MariaDB 10.4 can no longer be installed in 3.x. If you still run databases on 10.4, export them now and restore
    them into a newer MariaDB version afterwards.

### Verify your dumps

A broken dump is only noticed once you need it, so check the archives before you continue:

```bash
# all archives readable?
gzip -t ~/valet-sh-2x-backup/*.sql.gz

# every dump should end with "Dump completed"
zcat ~/valet-sh-2x-backup/mysql80-projectx.sql.gz | tail -3

# and it should not be suspiciously small
ls -lh ~/valet-sh-2x-backup/
```

### Elasticsearch and OpenSearch

Search indexes are derived data. Instead of backing them up, rebuild them from your application after the upgrade,
e.g. for Magento 2:

```bash
bin/magento indexer:reindex
```

If you really need the raw index data, create a snapshot via the Elasticsearch snapshot API before the upgrade. Note
that restoring such a snapshot into a container requires a manually mounted snapshot repository and is not covered
by valet.sh.

### Redis and Valkey

Redis and Valkey are used as caches, so there is normally nothing worth keeping - after the upgrade the cache simply
fills up again. If you do store non-reproducible data in Redis, save it while you are still on 2.x:

```bash
redis-cli -h 127.0.0.1 -p 6379 --rdb ~/valet-sh-2x-backup/redis6.rdb
```

### RabbitMQ

Queue contents are not worth preserving, but your definitions (vhosts, users, permissions, exchanges, queues,
bindings) are. Export them from the management interface:

```bash
curl -u guest:guest https://rabbitmq.test/api/definitions \
  > ~/valet-sh-2x-backup/rabbitmq-definitions.json
```

### Mails

Mails caught by Mailhog or Mailpit are test data and are not backed up.

### Your projects

Your project directories are untouched by the upgrade, including their `.valet-sh.yml`. Two things are worth writing
down anyway:

* which projects are linked, and with which PHP version (`valet.sh links` from *[step 1](#1-take-stock-of-your-current-setup)*)
* any manual changes you made to valet.sh-managed configuration files (php.ini snippets, Xdebug settings, ...), as
  those files are re-created during the upgrade

## 3. Switch to the 3.x release channel

!!! warning
    Make sure your operating system is supported by 3.x **before** you switch: macOS 26 or newer on Apple Silicon,
    or Ubuntu 24.04 / 26.04 - see *[Support-Matrix](support-matrix.md)*. Update your operating system first if
    needed, and remember that Intel Macs have to stay on 2.x.

Switching the release channel moves your installation to 3.x:

```bash
valet.sh release-channel 3.x
```

Afterwards, apply the 3.x baseline:

```bash
valet.sh install
```

!!! note
    After this step only the essential services (`nginx`, `dnsmasq`, `mailpit`) are installed - this is expected.
    Your old 2.x data directories are still on disk, but the services that could read them are gone, which is why
    the dumps from *[step 2](#2-back-up-your-data)* are the only reliable way to get your data back.

## 4. Install the services you need

Use the list from *[step 1](#1-take-stock-of-your-current-setup)* and install the same set of services again:

```bash
valet.sh install php83,mysql80,elasticsearch7
```

For a project with a *[.valet-sh.yml](../how-to-articles/project-configuration-via-valet-sh-yml.md)* you can let
valet.sh do it for you - `init-instance` installs every service version the file declares:

```bash
cd /path/to/your/project
valet.sh init-instance
```

Then set the defaults you had before, e.g.:

```bash
valet.sh service default php83
valet.sh service default mysql80
valet.sh service default elasticsearch7
```

## 5. Restore your data

### MySQL and MariaDB

Into the **default** database service:

```bash
valet.sh db import ~/valet-sh-2x-backup/mysql80-projectx.sql.gz projectx
```

Into a specific version - the clients run inside the container, so no host or port is needed:

```bash
mysql8.0 -e "CREATE DATABASE IF NOT EXISTS projectx"
zcat ~/valet-sh-2x-backup/mysql80-projectx.sql.gz | mysql8.0 projectx
```

!!! note
    A client only works while its service is running. If you see `Error: vsh-mysql80 is not running`, start it with
    `valet.sh service start mysql80`.

### RabbitMQ

Import the definitions you exported, using the web interface of the version you installed (e.g.
`rabbitmq313.test` for RabbitMQ 3.13):

```bash
curl -u guest:guest -H "Content-Type: application/json" -X POST \
  -d "@${HOME}/valet-sh-2x-backup/rabbitmq-definitions.json" \
  https://rabbitmq313.test/api/definitions
```

### Search indexes and caches

Rebuild them from your application, e.g. `bin/magento indexer:reindex` for Magento 2. Caches need no action.

### Projects

Link your projects again and, if you use the *[init-instance](../commands/init-instance.md)* workflow, let it set up
the project environment:

```bash
valet.sh link myproject php83
```

## 6. Update your project configuration (macOS only)

On Ubuntu nothing needs to change. On macOS, only the default database and the default search engine are available
on `127.0.0.1`. Every other version has to be addressed by its container name:

| Old setting (2.x) | New setting (3.x, macOS) |
|-------------------|--------------------------|
| 127.0.0.1:3306 (default database) | unchanged |
| 127.0.0.1:9200 (default search engine) | unchanged |
| 127.0.0.1:3308 | vsh-mysql80.vsh:3308 |
| 127.0.0.1:9207 | vsh-elasticsearch7.vsh:9207 |
| 127.0.0.1:6379 | vsh-redis6.vsh:6379 |
| 127.0.0.1:5674 | vsh-rabbitmq313.vsh:5674 |

Typical places to check: Magento's `app/etc/env.php`, Neos' `Settings.yaml`, `.env` files and any database or
search client configuration of your own. `localhost` still does not work - use `127.0.0.1` or the container name.

!!! note
    Files generated by valet.sh itself (e.g. the `env.php` written by *[init-instance](../commands/init-instance.md)*)
    already contain the correct host.

## Clean up 2.x leftovers

Your 2.x data directories are not deleted by the upgrade. Once you have verified that everything works again, you
can reclaim that disk space. Typical locations:

| Service | macOS | Ubuntu |
|---------|-------|--------|
| MySQL 8.0 | /usr/local/var/vsh-mysql80 | /usr/local/valet-sh/packages/mysql80/data |
| MariaDB 10.6 | /usr/local/var/vsh-mariadb106 | /usr/local/valet-sh/packages/mariadb106/data |
| Elasticsearch 7 | /usr/local/valet-sh/packages/elasticsearch7/data | /usr/local/valet-sh/packages/elasticsearch7/data |

!!! warning
    Deleting these directories is irreversible. Only do it after you have restored your data and confirmed that your
    projects work.

## Troubleshooting

**A client reports that the container is not running.**
Check the state of your services with `valet.sh service list` and start the one you need,
e.g. `valet.sh service start mysql80`.

**A port is already in use after the upgrade.**
A leftover 2.x service is probably still running. On macOS check `brew services list`, on Ubuntu
`systemctl --user list-units 'vsh-*'`, and stop whatever still occupies the port.

**A service is installed but not reachable from my application.**
On macOS, verify whether you are addressing a non-default version via `127.0.0.1` - see
*[step 6](#6-update-your-project-configuration-macos-only)*.

**Something is broken after the upgrade.**
Re-run `valet.sh install` to repair the essential stack. This re-applies the provisioning and does not touch your
data.

## See also

* *[What's new in valet.sh 3.x](whats-new.md)*
* *[Support-Matrix](support-matrix.md)*
* *[Services](../services/index.md)*
* *[install](../commands/install.md)* / *[uninstall](../commands/uninstall.md)* / *[service](../commands/service.md)*
* *[db](../commands/db.md)*
