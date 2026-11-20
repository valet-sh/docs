---
hide:
- footer
---

# How to use the development branch of valet.sh

Each new version is first tested in the `next` release channel before it is released to the stable `3.x` channel.
Follow the steps to switch an existing valet.sh 3.x installation to the `next` channel:

```bash
valet.sh release-channel
```

Select `next (development)` and apply the changes afterwards:

```bash
valet.sh install
```


Updates can be executed with the standard upgrade command
```bash
valet.sh self-upgrade
```

To switch back, run `valet.sh release-channel` again and select `3.x (Stable)`.
