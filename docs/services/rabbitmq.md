---
hide:
- footer
---

# RabbitMQ

RabbitMQ is optional and not installed by default - install the version you need via *[install](../commands/install.md)*,
e.g. `valet.sh install rabbitmq312`. You can install and run multiple versions at the same time, as different TCP
ports are used.

Both operating systems run the services in containers. On Ubuntu, Podman is used with the host network, so a service
stays reachable via `127.0.0.1` and its port. On macOS, each service runs as an Apple container with its own IP
address and is reachable via its DNS name in the `.vsh` domain, using the same port.

| Version | Protocol | Ubuntu | macOS |
|---------|----------|--------|-------|
| 3.12    | AMQP       | 127.0.0.1:5673   | vsh-rabbitmq312.vsh:5673   |
| 3.12    | Management | 127.0.0.1:15673  | vsh-rabbitmq312.vsh:15673  |
| 3.13    | AMQP       | 127.0.0.1:5674   | vsh-rabbitmq313.vsh:5674   |
| 3.13    | Management | 127.0.0.1:15674  | vsh-rabbitmq313.vsh:15674  |
| 4.0     | AMQP       | 127.0.0.1:5675   | vsh-rabbitmq40.vsh:5675    |
| 4.0     | Management | 127.0.0.1:15675  | vsh-rabbitmq40.vsh:15675   |
| 4.1     | AMQP       | 127.0.0.1:5676   | vsh-rabbitmq41.vsh:5676    |
| 4.1     | Management | 127.0.0.1:15676  | vsh-rabbitmq41.vsh:15676   |
| 4.2     | AMQP       | 127.0.0.1:5677   | vsh-rabbitmq42.vsh:5677    |
| 4.2     | Management | 127.0.0.1:15677  | vsh-rabbitmq42.vsh:15677   |
| 4.3     | AMQP       | 127.0.0.1:5678   | vsh-rabbitmq43.vsh:5678    |
| 4.3     | Management | 127.0.0.1:15678  | vsh-rabbitmq43.vsh:15678   |

The <strong>rabbitmq_management</strong> plugin is installed by default for every version. You can reach a version's
web interface at its management port, e.g. *[https://127.0.0.1:15673](https://127.0.0.1:15673)* for RabbitMQ 3.12.
Use `guest` as the username and `guest` as the password to log in.

Manage an installed version the same way as any other service:
```bash
valet.sh service enable rabbitmq312
valet.sh service disable rabbitmq312
```
