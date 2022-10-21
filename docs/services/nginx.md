---
hide:
- footer
---

# Nginx


## Configuration
All site configurations are stored in <strong>/etc/nginx/conf.d/</strong> (Linux) or <strong>/usr/local/etc/nginx/conf.d/</strong> (macOS) directory. Only files with .conf extension will be respected.

!!! Info
    You can add or modify those configuration files by your self, but commands like `valet.sh unlink` or `valet.sh link` can delete or override your changes!


## SSL
during the `valet.sh install` process a development CA will be created. To add the CA to your browsers trust chain, execute the following command.

```bash
valet.sh update-dev-ca
```

!!! Info
    after installing a new browser it may be necessary to re-run this command!

For each nginx site configuration created by `valet.sh link` a certificate signed by that CA will be created. This certificate covers the domain plus subdomains. A site created by `valet.sh link example` covers `example.test` and `*.example.test`.

