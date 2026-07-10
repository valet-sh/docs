# valet.sh Documentation

## local development

install required dependencies
```bash
pip3 install mkdocs-material
pip3 install mkdocs-awesome-pages-plugin
pip3 install mkdocs-redirects
pip3 install mike
```

run command in project root
```bash
mkdocs serve
```

open `http://127.0.0.1:8000/` in your browser

## versioning

Docs are versioned with [mike](https://github.com/jimporter/mike), mirroring the
`2.x`/`3.x` branches of the main [valet-sh](https://github.com/valet-sh/valet-sh) project:

- `master` → built and deployed as version `2.x`, aliased `latest` (default version shown to visitors)
- `3.x` → built and deployed as version `3.x` (available via the version dropdown, not yet default)

Deployment happens automatically via CI (`.github/workflows/ci.yml`) on push to either branch.
To preview the versioned site locally instead of the live `mkdocs serve` preview:

```bash
mike deploy 2.x latest   # or: mike deploy 3.x
mike serve
```

Once 3.x is ready to become the primary version, update the CI job to alias `3.x` as `latest`
and run `mike set-default --push 3.x`.



