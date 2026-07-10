---
hide:
- footer
---

# Install

## Description

Installs services on your machine. Only a small set of services (currently `nginx`, `dnsmasq` and `mailpit`) is
essential and always installed - everything else (PHP, MySQL, MariaDB, Elasticsearch, OpenSearch, Redis, Valkey,
RabbitMQ, Node.js, Composer, Magerun, ...) is optional and only installed when you explicitly ask for it, either
via this command or automatically on demand by *[init-instance](init-instance.md)* based on your project's
*[.valet-sh.yml](../how-to-articles/project-configuration-via-valet-sh-yml.md)*.

If valet.sh triggers errors, please re-run this command without arguments to repair/re-install the essential stack.
You may want to *[upgrade to the newest version](self-upgrade.md)* before.

## Usage

Install (or repair) only the essential baseline stack:
``` bash
valet.sh install
```

Install one or more specific, optional services in addition to the essential stack:
``` bash
valet.sh install php81,mysql57,elasticsearch7
```

!!! note
    See the *[Service command](service.md)* to enable/disable, start/stop or set the default version
    for an installed service, and *[Uninstall](uninstall.md)* to remove one again.
