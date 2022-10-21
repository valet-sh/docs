---
hide:
- footer
---

# DB

## Description

Create, drop, import, export, ls, reset of mysql databases

!!! note

    The commands are only executed on the default mySQL database server. You must change the default database if you want to work with these commands. Read more about how to change the default MySQL service *[here](https://valet.sh/commands/service)*.

## Usage

``` bash
valet.sh db (ls|create|drop|reset|export|import) (optional)<filename> <database-name>
```

## Examples

list all existing databases
``` bash
valet.sh db ls
```
create a new database
``` bash
valet.sh db create projectX
```
drops an existing database
``` bash
valet.sh db drop projectX
```
dops and creates a database
``` bash
valet.sh db reset projectX
```
import a mysql database dump. Database will be created if it does not exist
``` bash
valet.sh db import database.sql.gz projectX
```
export a mysql database into given db-filename
``` bash
valet.sh db export database.sql.gz projectX
```

