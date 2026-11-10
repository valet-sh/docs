---
hide:
- footer
---

# How to use the development branch of valet.sh

Each new version is first tested in the "next" branch. Follow the steps to switch to the next branch:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/valet-sh/install/3.x/install.sh)

valet.sh release-channel 3.x
valet.sh install
```


Updates can be executed with the standard upgrade command
```bash
valet.sh self-upgrade
```

