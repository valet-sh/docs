---
hide:
- footer
---

# Xdebug


## Description

Enables or disables xdebug for the defined PHP version.

## Usage

``` bash
valet.sh xdebug (on|off) <php_version>
 
  php_version: (5.6|7.0|7.1|7.2|7.3|7.4|8.0|8.1)
```
!!! note

    As of Version 2.1 the command will attempt to determine the target PHP version from .valet-sh.yml, thus making the parameter php_version optional.
    In case the parameter is not specified and the target PHP version cannot be determined, an error message will be issued, stating that the PHP version must be specified.


## Example Output

Enable xdebug for php5.6 on cli and fpm
``` bash
valet.sh xdebug on 5.6
```

Disable xdebug for php5.6 on cli and fpm
``` bash
valet.sh xdebug off 5.6
```