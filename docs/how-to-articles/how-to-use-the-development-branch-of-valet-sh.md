---
hide:
- footer
---

# How to use the development branch of valet.sh

Each new version is first tested in the "next" branch. Follow the steps to switch to the next branch:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/valet-sh/install/next/install.sh)

/usr/local/valet-sh/installer/valet-sh-installer release-channel next
valet.sh self-upgrade
valet.sh install
```


Updates can be executed with the standard upgrade command
```bash
valet.sh self-upgrade
```

use the following commands to switch back to the stable release branch
```bash
/usr/local/valet-sh/installer/valet-sh-installer release-channel 2.x
valet.sh self-upgrade
valet.sh install
```
