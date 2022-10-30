---
hide:
- footer
---

# Link

## Description

Linking of projects including automatic provisioning of nginx vhosts for a specific web application (e.g. magento). See also *[unlink](/commands/unlink)*.

## Usage

``` bash
valet.sh link <link-name> (optional)<php-version)
```

## Drivers

At the moment we are supporting the following php based applications. The link command tries to find out which web application it is and loads the corresponding nginx configuration.

Currently supported applications:

* Magento2
* Magento1
* Neos CMS
* Typo3 CMS
* Shopware 6

If no supported application was found, a minimal configuration is loaded!

!!! note

    do you need another one? Open a github issue! *[https://github.com/valet-sh/valet-sh](https://github.com/valet-sh/valet-sh)*

## Examples

Link the current directory with name 'projectx'. if you don't specify a php version, php72 will be used
``` bash
valet.sh link projectx
```
Link the current directory with a custom php version. Only the following values are allowed: php56 php70 php71 php72 php73 php74
``` bash
valet.sh link projectx php73
```