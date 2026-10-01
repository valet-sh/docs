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

| Type   | Version | Ubuntu           | macOS                  |
|--------|---------|------------------|------------------------|
| Redis  | 6       | 127.0.0.1:6380   | vsh-redis6.vsh:6380    |
| Redis  | 7       | 127.0.0.1:6381   | vsh-redis7.vsh:6381    |
| Valkey | 8       | 127.0.0.1:6389   | vsh-valkey8.vsh:6389   |
| Valkey | 9       | 127.0.0.1:6390   | vsh-valkey9.vsh:6390   |

!!! Info
    On macOS every installed cache version is additionally proxied to `127.0.0.1` on the same port (e.g.
    `127.0.0.1:6389` for Valkey 8), and the current default of the `cache` family is reachable via TCP port
    <strong>6379</strong>.

!!! Warning
    Unlike in 2.x, no cache service listens on port <strong>6379</strong> on Ubuntu - always use the version
    specific port there.

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

### Version specific CLI

For every installed version valet.sh provides a version specific CLI command. It runs `redis-cli`/`valkey-cli`
inside the corresponding container and already points at the right port, so you don't have to pass `-h`/`-p`
yourself.

| Type   | Version | CLI command   |
|--------|---------|---------------|
| Redis  | 6       | `redis6-cli`  |
| Redis  | 7       | `redis7-cli`  |
| Valkey | 8       | `valkey8-cli` |
| Valkey | 9       | `valkey9-cli` |

```bash
# open an interactive session on Valkey 8
valkey8-cli

# run a single command against Redis 7
redis7-cli ping

# the commands take all redis-cli/valkey-cli arguments
valkey8-cli --scan --pattern 'zend_cache*'
```

!!! Warning
    The commands execute inside the running container. If the service is stopped or disabled, they abort with
    `Error: vsh-valkey8 is not running` - start it first, e.g. via `valet.sh service enable valkey8`.

### Default CLI

In addition there are the plain `redis-cli` and `valkey-cli` commands. They do not connect on their own but
forward to one of the version specific commands above:

1. if a `.valet-sh.yml` exists in the current or parent directory and declares a
   *[services > redis > version](../how-to-articles/project-configuration-via-valet-sh-yml.md)* resp.
   `services > valkey > version`, the CLI of exactly that version is used
2. otherwise the current default of the `cache` family is used

```bash
cd ~/projects/myproject   # .valet-sh.yml declares services > valkey > version: "8"
valkey-cli                # → valkey8-cli
```

!!! Info
    Use the version specific command (`valkey8-cli`, `redis6-cli`, ...) whenever you want to be sure which
    instance you are talking to - `valet.sh service list` shows which version is currently the default.
