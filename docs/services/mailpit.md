---
hide:
- footer
---

# Mailpit

!!! Quote
    "An email and SMTP testing tool with API for developers" - please visit *[https://github.com/axllent/mailpit](https://github.com/axllent/mailpit)* for more information.

!!! Information
    Mailpit is part of the essential baseline stack and always installed - it cannot be uninstalled.


## Usage

You can access the UI via *[https://mailpit.test](https://mailpit.test)*

PHP is configured to use mailpit automatically (e.g. the mail() function), but you can also connect directly via SMTP.

On Ubuntu, the service runs directly on the host and is reachable via `127.0.0.1` and its port. On macOS, the
service runs as an Apple container and is additionally reachable via DNS on the `vsh-services` network, using the
same port.

| Protocol | Ubuntu | macOS |
|----------|--------|-------|
| HTTP (UI) | 127.0.0.1:8025 | vsh-mailpit.vsh-services:8025 |
| SMTP      | 127.0.0.1:1025 | vsh-mailpit.vsh-services:1025 |

![Image title](../assets/mailhog.png){ align=left }
