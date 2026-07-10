---
hide:
- footer
---

# What's new in valet.sh 3.x

!!! warning
    valet.sh 3.x is still under active development - this page and the rest of the 3.x documentation may change
    without notice. Use the version selector above to switch back to the current stable 2.x documentation.

The biggest change in 3.x is that most services are now **optional** and installed/removed on demand instead of
being bundled with every installation:

* Only a small essential baseline (`nginx`, `dnsmasq`, `mailpit`) is installed automatically - see *[Services](../services/index.md)*.
* Everything else (PHP, MySQL, MariaDB, Elasticsearch, OpenSearch, Redis, Valkey, RabbitMQ, Node.js, Composer, Magerun)
  is installed only when you ask for it, via *[install](../commands/install.md)*.
* New *[uninstall](../commands/uninstall.md)* command to remove a service you no longer need.
* *[init-instance](../commands/init-instance.md)* automatically installs whatever service versions your project's
  *[.valet-sh.yml](../how-to-articles/project-configuration-via-valet-sh-yml.md)* declares, if they aren't installed yet.
* Mailhog has been fully replaced by *[Mailpit](../services/mailpit.md)*, which is now part of the essential baseline.

See also *[Changelog](../changelog.md)*.

---

# What's new in valet.sh 2.x

Here is a short list of all the new main features of valet.sh 2.x (compared to 1.x).

* macOS Support
* parallel installation of MySQL 5.7 and 8.0
* New "service" command:
    * Manage the state of each service (enable/disable)
    * Manage a default service for PHP, Elasticsearch and MySQL (more information)