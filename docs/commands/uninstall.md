---
hide:
- footer
---

# Uninstall

## Description

Uninstalls one or more previously installed services from your machine again.

## Usage

Uninstall one or more specific, optional services:
``` bash
valet.sh uninstall php81,mysql57,elasticsearch7
```

Uninstall **everything**, including the essential services (`nginx`, `dnsmasq`, `mailpit`) - i.e. a complete
removal of valet.sh from your machine:
``` bash
valet.sh uninstall --all
```

!!! warning
    Running `valet.sh uninstall` without any arguments does nothing - you must either name at least one service
    or pass `--all`.

    `--all` removes **all** services, including the essential ones - this is a full uninstall of valet.sh itself,
    not just a cleanup of optional services.

!!! note
    See the *[Install](install.md)* and *[Service](service.md)* commands to (re-)install a service
    or manage the state of an already installed one.
