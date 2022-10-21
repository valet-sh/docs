---
hide:
- footer
---

# Install IonCube Loader


## MacOS

Example for PHP7.4
```bash
cd /tmp
curl https://downloads.ioncube.com/loader_downloads/ioncube_loaders_mac_x86-64.zip -o ioncube.zip
unzip ioncube.zip
rm ioncube.zip
sudo cp ioncube/ioncube_loader_mac_7.4.* /usr/local/Cellar/vsh-php74/7.4.*/lib/vsh-php74/20*/
rm -rf ioncube
sudo echo "zend_extension=ioncube_loader_mac_7.4.so" > /usr/local/etc/vsh-php74/conf.d/ext-ioncube.ini
valet.sh service restart php74
```

