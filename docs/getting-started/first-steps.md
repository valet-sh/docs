---
hide:
- footer
---

# First steps

## Development SSL Certificates

make sure the development CA has been imported into your browser. To test this, just go to <strong>https://mailpit.test</strong> in your browser.  You shouldn't get a certificate warning from your browser.    If you have any issue please try to start the certificate import manually.

!!! Warning
    Under Ubuntu, the certificate must be imported separately into each browser.  If you install a new browser, you must import the certificate with this command.

``` bash
valet.sh update-dev-ca
```


## Install and manage the services you need

A fresh installation only comes with the essential baseline (`nginx`, `dnsmasq`, `mailpit`) - no PHP, database,
search engine, cache or anything else is installed yet. Install only what you actually need:

``` bash
valet.sh install php81,mysql57,elasticsearch7
```

Once a service is installed, use <strong>valet.sh service list</strong> to see all installed services and their
state. Use <strong>valet.sh service enable <service></strong> respectively <strong>valet.sh service disable <service></strong> to enable or disable one, and <strong>valet.sh service default <service></strong> to set a service as the default for its family, e.g.:

``` bash
# select php81 as default version. If you run "PHP" on the console you will automatically get PHP 8.1. All other installed versions can still be reached via the version e.g. php7.4
valet.sh service default php81
 
# select elasticsearch7 as default version. Elasticsearch 7 now running on port 9200, but all other version can still be reached via their own ports
valet.sh service default elasticsearch7
 
# select mysql57 as default version. MySQL 5.7 now running on port 3306 and you will reach it on CLI automatically via "mysql"
valet.sh service default mysql57
```

If you have any questions about the available services or versions, please check out the *[service documentation](../services/index.md)*.


