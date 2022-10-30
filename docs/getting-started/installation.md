---
hide:
- footer
---

# Installation

!!! Info "Migration from valet+"
    If you are migrating from valet+, please migrate with the *[macOS Upgrade Guide guide](/how-to-articles/migrate-from-valet-plus-to-valet-sh)*.


## Install valet.sh

``` bash
bash <(curl -fsSL https://raw.githubusercontent.com/valet-sh/install/master/install.sh)
```


!!! Warning "Installation on Apple M1"
    At the moment valet.sh on Apple m1 requires rosetta2

    ``` bash
    /usr/sbin/softwareupdate --install-rosetta --agree-to-license
    bash <(curl -fsSL https://raw.githubusercontent.com/valet-sh/install/master/install.sh)
    ```


Reopen your terminal and install all services and tools via

``` bash
valet.sh install
```

## Next see *[First-Steps](/getting-started/first-steps)*