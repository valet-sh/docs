---
hide:
- footer
---

# Composer

## Versions

|Version|Path| Plugins           | Default version         |
|-------|-----|-------------------|-------------------|
|composer1.x|/usr/local/bin/composer1| hirak/prestissimo |YES|
|composer2.x|/usr/local/bin/composer2|                   |NO|



## Change the default version
to change the default version of composer when using the "composer" command (without the version suffix at the end) on cli, you need to change it via valet.sh

change the default composer version to 2
```bash
valet.sh service default composer2
```

composer 2 is now your default version

![Image title](/assets/valet-sh-composer2.png){ align=left }