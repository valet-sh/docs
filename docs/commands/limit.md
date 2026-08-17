---
hide:
- footer
---

# Limit

## Description

cpus, memory, get, remove, manages entries in the config file for each service.
This is used to limit the resources available to each service.

## Usage

``` bash
valet.sh limit (cpus|memory) <value> <service-name>
valet.sh limit (get|remove) (cpus|memory) <service-name>
```

## Examples

set the cpu limit for a service
``` bash
valet.sh limit cpus 2 opensearch2
```
set the memory limit for a service
``` bash
valet.sh limit memory 2g opensearch2
```
show the cpu limit for a service
``` bash
valet.sh limit get cpus opensearch2
```
show the memory limit for a service
``` bash
valet.sh limit get memory opensearch2
```
remove the cpu limit for a service
``` bash
valet.sh limit remove cpus opensearch2
```
remove the memory limit for a service
``` bash
valet.sh limit remove memory opensearch2
```
