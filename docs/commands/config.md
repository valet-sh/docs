---
hide:
- footer
---

# Config

## Description

Sets, deletes, manages config entries in the local global valet.sh config file

## Usage

``` bash
valet.sh config (list|get|set|remove) <variable-name> <variable-value>
```

## Examples

list all custom valet.sh variables
``` bash
valet.sh config list
```
get a single variable value
``` bash
valet.sh config get varname
```
set a valet.sh variable
``` bash
valet.sh config set varname varvalue
```
delete a custom valet.sh variable
``` bash
valet.sh config remove varname
```

## Available configurations

| config var | default value  | allowed values | comment |
|----------- |-----------|-------------|------------|
| default_shell | zsh | bash,zsh | "valet.sh install" is required after changing the configuration |
