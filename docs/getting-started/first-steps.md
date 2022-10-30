---
hide:
- footer
---

# First steps

## Development SSL Certificates

make sure the development CA has been imported into your browser. To test this, just go to <strong>https://mailhog.test</strong> in your browser.  You shouldn't get a certificate warning from your browser.    If you have any issue please try to start the certificate import manually.

!!! Warning
    Under Ubuntu, the certificate must be imported separately into each browser.  If you install a new browser, you must import the certificate with this command.

``` bash
valet.sh update-dev-ca
```


## Manage your needed services

valet.sh comes with a bunch of services that can require a lot amount of RAM and CPU.
Therefor you should disable/enable only the services you really need. Use <strong>valet.sh service list</strong> to get a list of all services and their states. Use <strong>valet.sh service enable <service></strong> respectively <strong>valet.sh service disable <service></strong>  enable or disable a service.

You can find more information about handling service status *[here](/services)*.

``` bash
# select php7.4 as default version. If you run "PHP" on the console you will automatically get PHP 7.4. All other versions can still be reached via the version e.g. php7.2
valet.sh service default php74
 
# select elasticsearch7 as default version. Elasticsearch 7 now running on port 9200, but all other version can still be reached via their own ports
valet.sh service default elasticsearch7
 
# select mysql80 as default version. MySQL 8.0 now running on port 3306 and you will reach it on CLI automatically via "mysql"
valet.sh service default mysql80
```

If you have any questions about the available services or versions, please check out the *[service documentation](/services)*.


