---
hide:
- footer
---

# Migration-Cheatsheet from valet-plus to valet.sh

!!! Note "Information"
    Most of the commands from valet-plus can be used in the same way with "valet.sh" instead of "valet" (see also Commands).
    Please refer to the following cheatsheet to determine if you need to change your workflow.

## Commands

---
### valet use 7.4

<strong>New Command: php7.4 (see Comment)</strong>

<strong>Comment:</strong>

With valet+ you needed to switch PHP versions on CLI every time you needed to do a change within a project with a different PHP version.   
With valet.sh now all PHP versions are installed at the same time. 

* <strong>CLI:</strong> To use PHP 7.1 on cli, simply enter "php7.1 {your command}". For composer install on 7.3 for example you can use "php7.3 $(which composer1) install". 
    * You can also use the .valet-sh.yml to specify the PHP version for the current folder. 
* <strong>WEB:</strong> The PHP version that is used within the web (browser) is specified in the corresponding link (see valet.sh link).
  
If you need to change your default PHP CLI version, you can use "valet.sh service default php72" to change your default PHP to 7.2 without the need to specify a version.  
This usage is NOT RECOMMENDED and should be avoided. Please switch to the explicit PHP version specification where possible, especially in project instantiation scripts.

---
### valet xdebug on

<strong>New Command: valet.sh xdebug on 7.4</strong>

<strong>Comment:</strong>

You now need to specify the PHP version.


---
### valet link myproject --secure

<strong>New Command:</strong> valet.sh link myproject php74

<strong>Comment:</strong>

You now need to specify the PHP version.


---
### valet db create myproject


<strong>New Command:</strong> `valet.sh db create myproject` (with default mySQL) or `mysql8.0 -e 'CREATE DATABASE myproject'` (for a specific mySQL version)

<strong>Comment:</strong> You now may need to specify the mySQL version (mysql5.7 / mysql8.0).

---
### valet db drop myproject


<strong>New Command:</strong> `valet.sh db drop myproject` (with default mySQL) or `mysql8.0 -e 'DROP SCHEMA IF EXISTS myproject'` (for a specific mySQL version)

<strong>Comment:</strong> You now may need to specify the mySQL version (mysql5.7 / mysql8.0).

---
### valet db dump myproject myproject


<strong>New Command:</strong> `valet.sh db export myproject` (with default mySQL) or `mysqldump8.0 --default-character-set=utf8 --single-transaction --no-tablespaces -uroot -p -h127.0.0.1 --port=3308 myproject | gzip > myproject.sql.gz` (for a specific mySQL version)

<strong>Comment:</strong>

Use port 3307 for mySQL 5.7, use port 3308 for mySQL 8.  
You now may need to specify the mySQL version (mysqldump5.7 / mysqldump8.0).
---
### valet db import myproject.sql myproject

<strong>New Command:</strong> `valet.sh db import myproject` (with default mySQL) or `mysql8.0 -e 'CREATE DATABASE myproject'` (for a specific mySQL version)

<strong>Comment:</strong> You now may need to specify the mySQL version (mysql5.7 / mysql8.0).

---
### valet.sh install elasticsearch 7

<strong>New Command:</strong> `valet.sh service enable elasticsearch7`

<strong>Comment:</strong> The most Elasticsearch versions are pre-installed. Simply enable them to use them.


---
### valet restart nginx

<strong>New Command:</strong> `valet.sh service restart nginx`

---
### mysql

<strong>New Command:</strong> `mysql8.0` or `mysql5.7` or `mariadb10.4`


## Project configuration changes:

| Old Setting | New setting |Description|
|-------------|-------------|----------|
| localhost   | 127.0.0.1   | Please change all usages of localhost to 127.0.0.1|
|localhost / 3306	|127.0.0.1 / 3307|If you use the port 3306 for your project's db configuration, please change it to 3307 for mySQL 5.7 or 3308 for mySQL 8.|
|localhost / 9200		|127.0.0.1 / 9207|If you use the port 3306 for your project's db configuration, please change it to 3307 for mySQL 5.7 or 3308 for mySQL 8.|