---
hide:
- footer
---

# Services

Most services are **optional**: valet.sh only installs a small, essential baseline on every machine, everything else
you install and uninstall yourself as needed, via *[install](../commands/install.md)* and *[uninstall](../commands/uninstall.md)*.

## Essential (always installed)

* *[Mailpit](mailpit.md)*
* *[Nginx](nginx.md)*
* dnsmasq (internal, not user-configurable)

## Optional (install on demand)

* *[Composer](composer.md)*
* *[Elasticsearch](elasticsearch.md)*
* *[MariaDB](mariadb.md)*
* *[MySQL](mysql.md)*
* *[NodeJS](nodejs.md)*
* *[OpenSearch](opensearch.md)*
* *[PHP](php.md)*
* *[Rabbitmq](rabbitmq.md)*
* *[Redis](redis.md)*
* *[Valkey](valkey.md)*

!!! note
    A project's *[.valet-sh.yml](../how-to-articles/project-configuration-via-valet-sh-yml.md)* can still declare which
    service versions it needs - *[init-instance](../commands/init-instance.md)* will install any of them automatically
    if they aren't installed yet. This applies to all project types (Magento2, AEM, Neos), though it may not yet be
    implemented for every one of them.