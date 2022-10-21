---
hide:
- footer
---

# Unlink


## Description

unlinking projects which means deleting vhosts configurations.


## Usage

``` bash
valet.sh unlink <link-name>
```
The command only deletes the nginx configuration for the given link-name. Other data will not be deleted!



## Example

``` bash
valet.sh unlink projectx
```
