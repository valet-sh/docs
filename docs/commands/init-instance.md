---
hide:
- footer
---

# Init-Instance

## Description

Sets up the project according to the .valet-sh.yml file in the current directory.
See also the init command to generate a plain configuration file and the Project configuration via .valet-sh.yml guide.

## Usage

``` bash
valet.sh init-instance
```

## Options

``` bash
--identifier      Set different database identifier (e.g. "test" is used within .valet-sh.yml but you want to use the "prod" database file, you can use --identifier=prod
--skip-db         Skip database synchronisation (downloading, dropping and importing the database file)
--skip-fs         Skip filesystem synchronisation (media files etc.)
```
