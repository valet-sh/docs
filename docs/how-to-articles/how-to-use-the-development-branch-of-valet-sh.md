---
hide:
- footer
---

# How to use the development branch of valet.sh

Each new version is first tested in the "next" branch. follow the steps to switch to the next branch:



## Ubuntu

```bash
cd /usr/local/valet-sh/valet-sh
git checkout next
git pull
source /usr/local/valet-sh/venv/bin/activate
pip3 install -I --upgrade setuptools==60.8.2 wheel==0.37.1
pip3 install -I -r "/usr/local/valet-sh/valet-sh/requirements.txt"
deactivate
cd
valet.sh install
```

## MacOS

```bash
cd /usr/local/valet-sh/valet-sh
git checkout next
git pull
source /usr/local/valet-sh/venv/bin/activate
pip3 install --upgrade setuptools==60.8.2 wheel==0.37.1
pip3 install -r "/usr/local/valet-sh/valet-sh/requirements.txt"
deactivate
cd
valet.sh install
```