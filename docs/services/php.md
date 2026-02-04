---
hide:
- footer
---

# PHP

## Versions
at the moment PHP 5.6, 7.0, 7.1, 7.2, 7.3, 7.4, 8.0, 8.1, 8.2, 8.3, 8.4 and 8.5 are installed by valet.sh


| Version | Linux socket                 | MacOS socket        | Servicename |xdebug 2.*|xdebug 3.*|FPM service running by default|
|---------|------------------------------|---------------------|-------------|------|-------|------|
| php-5.6 | /var/run/php/php5.6-fpm.sock | /tmp/vsh-php56.sock | php56       | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-xmark:{ .cross-mark } |
| php-7.0 | /var/run/php/php7.0-fpm.sock | /tmp/vsh-php70.sock | php70       | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-xmark:{ .cross-mark } |
| php-7.1 | /var/run/php/php7.1-fpm.sock | /tmp/vsh-php71.sock | php71       | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-xmark:{ .cross-mark } |
| php-7.2 | /var/run/php/php7.2-fpm.sock | /tmp/vsh-php72.sock | php72       | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-check:{ .check-mark } |
| php-7.3 | /var/run/php/php7.3-fpm.sock | /tmp/vsh-php73.sock | php73       | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-check:{ .check-mark } |
| php-7.4 | /var/run/php/php7.4-fpm.sock | /tmp/vsh-php74.sock | php74       | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-check:{ .check-mark } |
| php-8.0 | /var/run/php/php8.0-fpm.sock | /tmp/vsh-php80.sock | php80       | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } |
| php-8.1 | /var/run/php/php8.1-fpm.sock | /tmp/vsh-php81.sock | php81       | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } |
| php-8.2 | /var/run/php/php8.2-fpm.sock | /tmp/vsh-php82.sock | php82       | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } |
| php-8.3 | /var/run/php/php8.3-fpm.sock | /tmp/vsh-php83.sock | php83       | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } |
| php-8.4 | /var/run/php/php8.4-fpm.sock | /tmp/vsh-php84.sock | php84       | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } |
| php-8.5 | /var/run/php/php8.5-fpm.sock | /tmp/vsh-php85.sock | php85       | :fontawesome-solid-xmark:{ .cross-mark } | :fontawesome-solid-check:{ .check-mark } | :fontawesome-solid-xmark:{ .cross-mark } |


## manage services

to manage the state (enable/disable/start/stop) of each php version, use the service command (Read more about the service command *[here](/services)*).


```bash
# stop and disable php7.2
valet.sh service disable php72
 
# start and enable php5.6
valet.sh service enable php56
```

!!! Info
    disabling a php service stops only the FPM service for the selected version! You can still use all installed php versions on cli. (e.g "php5.6")


## Manage xdebug

### Versions
xdebug2 and xdebug3 are provided by valet.sh, but only php7.3 and php7.4 supports both xdebug major versions

change the default xdebug version
```bash
valet.sh service default xdebug3
```

### Example: change xdebug version from 3 to 2
Let's assume you are running xdebug3 on php7.4 and want to switch to xdebug2

* ensure xdebug is disabled for your desired php version
```bash
valet.sh xdebug off 7.4
```
* switch xdebug version
```bash
valet.sh service default xdebug2
```
* enable xdebug for php7.4
```bash
valet.sh xdebug on 7.4
```
* xdebug2 is now enabled for php7.4!

![Image title](/assets/valet-sh-xdebug-php74.png)


!!! Info
    Setting a "default" xdebug version has no effect on php versions that supports only <strong>one</strong> xdebug version. For example php8.0 will always load xdebug3 even when the default version is set to xdebug2!

