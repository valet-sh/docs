---
hide:
- footer
---

Every now and then we publish updates of valet.sh that you should adopt as fast as possible. In the past we often encountered the issue that people upgraded valet.sh  but did not seem to be able to use the newest features. Most of the time this was related to the two-step-upgrade required to actually roll out the upgrades on their machines not having been followed through.

To properly roll out the latest upgrade of valet.sh on your machine, always perform the two following steps in the mentioned order:

## Update only valet.sh

```bash
valet.sh self-upgrade
valet.sh install
```

The first step upgrades the code of your valet.sh copy (comparable to apt update on Debian based Linux distributions), the second makes sure that the ecosystem defined by valet.sh is applied to your machine (comparable to apt upgrade on Debian based Linux distributions).

In case you are missing a feature of valet.sh on your machine although it should be there, run valet.sh install and check whether the feature becomes available.


## Update System and valet.sh 

### Ubuntu

```bash
sudo apt-get update
sudo apt-get upgrade

valet.sh self-upgrade
valet.sh install
```

---
### MacOs (Intel)

```bash

brew update
brew uppgrade

valet.sh self-upgrade
valet.sh install
```

---
### MacOs (M1)

```bash

brew_x86 update
brew_x86 upgrade
brew update
brew upgrade

valet.sh self-upgrade
valet.sh install
```


