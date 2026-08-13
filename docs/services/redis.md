---
hide:
- footer
---

# Redis

Redis and Valkey belong to the same `cache` service family and are treated the same way as MySQL/MariaDB - both
are optional, not installed by default, and can be installed/run in parallel across versions and across each other,
since different TCP ports are used.

Install the version you need via *[install](../commands/install.md)*, e.g. `valet.sh install redis6` or
`valet.sh install valkey8`.

Both operating systems run the services in containers. On Ubuntu, Podman is used with the host network, so a service
stays reachable via `127.0.0.1` and its port. On macOS, each service runs as an Apple container with its own IP
address and is reachable via its DNS name in the `.vsh` domain, using the same port.

| Type   | Version | Ubuntu           | macOS                             |
|--------|---------|------------------|-------------------------------------|
| Redis  | 6       | 127.0.0.1:6379   | vsh-redis6.vsh:6379        |
| Redis  | 7       | 127.0.0.1:6380   | vsh-redis7.vsh:6380        |
| Valkey | 8       | 127.0.0.1:6389   | vsh-valkey8.vsh:6389       |
| Valkey | 9       | 127.0.0.1:6390   | vsh-valkey9.vsh:6390       |

## Manage services

Whichever version you install first becomes the default within the `cache` family unless you set a different one
via *[service default](../commands/service.md)*. You can start/stop and enable/disable each installed version via
valet.sh.

```bash
# stop and disable Redis 6
valet.sh service disable redis6
 
# start and enable Redis 6
valet.sh service enable redis6
 
# stop and disable Valkey 8
valet.sh service disable valkey8
 
# start and enable Valkey 8
valet.sh service enable valkey8
```

## Access Redis/Valkey

You can also use the cli tools to connect

```bash
redis-cli
valkey-cli
```
