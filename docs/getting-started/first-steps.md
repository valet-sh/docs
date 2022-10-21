---
hide:
- footer
---

# First steps

## Development SSL Certificates

make sure the development CA has been imported into your browser. To test this, just go to https://mailhog.test in your browser.  You shouldn't get a certificate warning from your browser.    If you have any issue please try to start the certificate import manually.

!!! Warning
    Under Ubuntu, the certificate must be imported separately into each browser.  if you install a new browser you have to import the certificate via the command provided command.

``` bash
valet.sh update-dev-ca
```


## Manage your needed services

valet.sh comes with a bunch of services that can require a lot amount of RAM and CPU.
Therefor you should disable/enable only the services you really need. Use <strong>valet.sh service list</strong> to get a list of all services and their states. Use <strong>valet.sh service enable <service></strong> respectively <strong>valet.sh service disable <service></strong>  enable or disable a service.

You can find more information about handling service status *[here](/services)*.

