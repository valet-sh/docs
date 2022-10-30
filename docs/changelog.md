---
hide:
- footer
---

# Changelog

## *[2.8.0 (19/09/2022)](https://github.com/valet-sh/valet-sh/releases/tag/2.8.0)*

<strong>Issues that have been solved</strong>

* mysql settings were not optimal (*[#226](https://github.com/valet-sh/valet-sh/issues/226)*)
* 'db' command does not support MariaDB (*[#224](https://github.com/valet-sh/valet-sh/issues/224)*)
* Python deprecation warning on Ubuntu 22.04 (*[#222](https://github.com/valet-sh/valet-sh/issues/222)*)
* broken .my.cnf symlink by setting mariadb10.4 as default service (*[#219](https://github.com/valet-sh/valet-sh/issues/219)*)


<strong>Changes</strong>

* ansible facts_cache enabled to increase execution speed (*[#238](https://github.com/valet-sh/valet-sh/issues/238)*)
* Neos/Flow flow_context is now configurable (*[#235](https://github.com/valet-sh/valet-sh/issues/235)*)
* Restart dnsmasq when using valet.sh service restart all (*[#218](https://github.com/valet-sh/valet-sh/issues/218)*)
* Restart Nginx when using valet.sh service restart all (*[#215](https://github.com/valet-sh/valet-sh/issues/215)*)
* Start correct PHP when linking projects (*[#213](https://github.com/valet-sh/valet-sh/issues/213)*)
* link command should not trigger an error (*[#80](https://github.com/valet-sh/valet-sh/issues/80)*)
* Add command to deploy env.php from .valet-sh.yml (*[#217](https://github.com/valet-sh/valet-sh/issues/217)*)
* Add comand to clear project specific cache (*[#216](https://github.com/valet-sh/valet-sh/issues/216)*)
* mysql and mysqldump binary respect specified DBMS in .valet-sh.yml files (*[#185](https://github.com/valet-sh/valet-sh/issues/185)*)
* PATH variable is now set in PHP-FPM services (*[#242](https://github.com/valet-sh/valet-sh/issues/242)*)


## *[2.7.0 (21/04/2022)](https://github.com/valet-sh/valet-sh/releases/tag/2.7.0)*

<strong>Issues that have been solved</strong>

* Invalid php temp dir detection on macOS (*[#188](https://github.com/valet-sh/valet-sh/issues/188)*)
* Fix error on init-instance filesystem sync when target directory does not exist (*[#190](https://github.com/valet-sh/valet-sh/issues/190)*)
* Allow the use of a test.php within Magento (*[#192](https://github.com/valet-sh/valet-sh/issues/192)*)
* Increase table width of links list (see commit)


<strong>Changes</strong>

* Support for Apple Silicon (via rosetta2) (*[#200](https://github.com/valet-sh/valet-sh/issues/200)*)
* macOS Monterey support (Intel and M1)
* Support for OpenSearch 1 (*[#198](https://github.com/valet-sh/valet-sh/issues/198)*)
* Support for ElasticSearch 8 (*[#204](https://github.com/valet-sh/valet-sh/issues/204)*)
* Post restore commands are now generic shell commands and not bound to php (*[#194](https://github.com/valet-sh/valet-sh/issues/194)*)
* Composer now runs in non-interactive mode (*[#189](https://github.com/valet-sh/valet-sh/issues/189)*)
* Up2date check (shows a warning if valet.sh self-upgrade was not executed for more than 30 days) (*[#48](https://github.com/valet-sh/valet-sh/issues/48)*)
* Add the option to skip DB synchronisation within init-instance (*[#202](https://github.com/valet-sh/valet-sh/issues/202)*)
* PHP version definition will now be passed through to sub folders (see commit)


## *[2.6.0 (29/11/2021)](https://github.com/valet-sh/valet-sh/releases/tag/2.6.0)*
<strong>Issues that have been solved</strong>

* (none)

<strong>Changes</strong>

* Dynamically use specified composer version (*[#174](https://github.com/valet-sh/valet-sh/issues/174)*)
* Add support for MariaDB via init-instance (*[#178](https://github.com/valet-sh/valet-sh/issues/178)*)
* Support for PHP8.1


## *[2.5.0 (29/10/2021)](https://github.com/valet-sh/valet-sh/releases/tag/2.5.0)*

<strong>Issues that have been solved</strong>

* valet.sh service command without an argument fails without correct error message (https://github.com/valet-sh/valet-sh/pull/169)

<strong>Changes</strong>

* Added a default vhost that shows all linked sites (https://github.com/valet-sh/valet-sh/pull/171)
* fuzzy service name inputs (php73, PHP7.3, php7.3) are now possible (https://github.com/valet-sh/valet-sh/pull/170)
* Updated Magento2 workflow for "Init-instance" command to allow processing custom cli commands and SQL-Queries (https://github.com/valet-sh/valet-sh/pull/168)
* .valet-sh.yml stub file now contains composer defintion as service (https://github.com/valet-sh/valet-sh/pull/167)
* MariaDB 10.4 service is now available (https://github.com/valet-sh/valet-sh/pull/176)


## *[2.4.0 (29/08/2021)](https://github.com/valet-sh/valet-sh/releases/tag/2.4.0)*

<strong>Issues that have been solved</strong>

* (none)

<strong>Changes</strong>

* xdebug3 is now available for PHP 7.3, 7.4 and 8.0 (please see PHP#Managexdebug)
* composer2 is now available (please see Composer)


## *[2.3.0 (24/08/2021)](https://github.com/valet-sh/valet-sh/releases/tag/2.3.0)*

<strong>Issues that have been solved</strong>

* Fix non-interactive Magento app:config:import (https://github.com/valet-sh/valet-sh/pull/158)
* Replace Elasticsuite specific indexes with reindexAll in stub file (https://github.com/valet-sh/valet-sh/pull/156)

<strong>Changes</strong>

* PHP8.0 is now available
* "valet.sh link" now supports typo3


## *[2.2.0 (02/08/2021)](https://github.com/valet-sh/valet-sh/releases/tag/2.2.0)*

<strong>Issues that have been solved</strong>

* (none)

<strong>Changes</strong>

* Neos-Workflows for "init-instance" and "restore" command are now available


## *[2.1.1 (05/07/2021)](https://github.com/valet-sh/valet-sh/releases/tag/2.1.1)*

<strong>Issues that have been solved</strong>

* invalid ansible version dependency


## *[2.1.0 (05/07/2021)](https://github.com/valet-sh/valet-sh/releases/tag/2.1.0)*

<strong>Issues that have been solved</strong>

* Using valet.sh link without php version will use the default php version #143
* Service disable fails with not started services #134

<strong>Changes</strong>

* PHP
    * "valet.sh xdebug on" is now working without specifing a PHP version when a .valet-sh.yml file exists in current directory
* Nginx
    * each vhost now uses its own access and error log file
* NodeJs
    * default node version is now 14


## *[2.0.1 (16/04/2021)](https://github.com/valet-sh/valet-sh/releases/tag/2.0.1)*

<strong>Issues that have been solved</strong>

* rabbitmq vhost queues not removeable via web interface #128
* A command to stub the .valet-sh.yml #47
* Automatically set PHP version #74
* Update env.php for magento 2.4 compatibility #103
* php imagick module is not installed #126
* Import of development CA on Ubuntu is slow #123
* valet.sh install fails after a certain time if the entered password was wrong #92
* Support for bash shell #51
* make zsh usage optional #117
* valet.sh init-instance website config is not configurable #107
* Restore does not work with provided parameters #105
* Switch composer installs in init-instance #130
* Install composer as root #95

<strong>Changes</strong>

* Shell
    * You can now use the Bash shell if you prefer (you needed to use zsh before)
    * Use this command to define Bash as your default shell: valet.sh configset default_shell bash
* RabbitMQ
    * The RabbitMQ "admin" user that will be created by default now has administrator privileges and will be able to delete VHosts via web interface
* PHP
    * The module "imagick" is now automatically installed
* Instanciation of projects
    * You can now use "valet.sh init" to create a .valet-sh.yml file that defines and sets up your environment (see documentation)
    * If you use the configuration via .valet-sh.yml and define a PHP version, you can now use "php" instead of the specific PHP version ("php7.4" etc.)
    * The env.php provided for magento projects via init-instance is now compatible with Magento 2.4(this command is currently alpha state and therefore not documented completely)
* Performance
    * The install process has been sped up on Ubuntu
* Bugfixes
    * valet.sh install will not fail anymore if it's taking too long to execute
    * Magento configuration in .valet-sh.yml will now work properly on website scope
    * The restore command will now work for other identifiers than test (this command is currently alpha state and therefore not documented yet)
    * composer is now installed as root and given ownership to the current user afterwards to ensure it can be overwritten in the future

    