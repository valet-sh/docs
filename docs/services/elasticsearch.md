---
hide:
- footer
---

# ElasticSearch

## Version

Elasticsearch and OpenSearch are optional and not installed by default - install the version(s) you need via
*[install](../commands/install.md)*, e.g. `valet.sh install elasticsearch7`. Versions 1,2,5,6,7 and 8 of Elasticsearch
and versions 1,2 and 3 of OpenSearch are supported. You can install and run each version at the same time, because
different TCP ports are used.

Both operating systems run the services in containers. On Ubuntu, Podman is used with the host network, so a service
stays reachable via `127.0.0.1` and its port. On macOS, each service runs as an Apple container with its own IP
address and is reachable via its DNS name in the `.vsh` domain, using the same port.

|Elasticsearch version|Ubuntu|macOS|
|-------------|--------|--------|
|1.x|127.0.0.1:9201|vsh-elasticsearch1.vsh:9201|
|2.x|127.0.0.1:9202|vsh-elasticsearch2.vsh:9202|
|5.x|127.0.0.1:9205|vsh-elasticsearch5.vsh:9205|
|6.x|127.0.0.1:9206|vsh-elasticsearch6.vsh:9206|
|7.x|127.0.0.1:9207|vsh-elasticsearch7.vsh:9207|
|8.x|127.0.0.1:9208|vsh-elasticsearch8.vsh:9208|


| OpenSearch version | Ubuntu | macOS |
|--------------------|----------|----------|
| 1.x                | 127.0.0.1:9221 | vsh-opensearch1.vsh:9221 |
| 2.x                | 127.0.0.1:9222 | vsh-opensearch2.vsh:9222 |
| 3.x                | 127.0.0.1:9223 | vsh-opensearch3.vsh:9223 |


!!! Info
    The default Elasticsearch/OpenSearch is also accessed via TCP port 9200!

## manage Elasticsearch services

Whichever version you install first becomes the default (also reachable via port 9200) unless you set a different
one via *[service default](../commands/service.md)*. You can start/stop and enable/disable each installed
elasticsearch version via valet.sh.

```bash
# stop and disable elasticsearch 5
valet.sh service disable elasticsearch5

# start and enable elasticsearch 5
valet.sh service enable elasticsearch5
```

## Update Elasticsearch

Each Elasticsearch/OpenSearch version is shipped as a container with a fixed image tag pinned by valet.sh itself
(e.g. `elasticsearch:8.19.18`) - there is no automatic or forced update mechanism for minor or patch level releases.
A newer patch/minor version only becomes available once a valet.sh release bumps that pinned tag.

To pick up such an update, first update valet.sh itself via *[self-upgrade](../commands/self-upgrade.md)*, then
re-run *[install](../commands/install.md)* for the affected version - since the service is already installed, this
re-pulls the (now updated) image and recreates the container.

Example commands for updating <strong>elasticsearch 5</strong>
```bash
valet.sh self-upgrade
valet.sh install elasticsearch5
```

!!! Info
    The service's data lives in a dedicated container volume, not in the container image, so updating to a newer
    pinned version does not delete your data.

If you want to fully reset a version instead, including its data, uninstall it with `--purge` and reinstall it:
```bash
valet.sh uninstall elasticsearch5 --purge
valet.sh install elasticsearch5
```

!!! Warning
    `--purge` removes the container volume, deleting all indexed data for the affected version irreversibly!

## Plugins

The plugins <strong>analysis-phonetic</strong> and <strong>analysis-icu</strong> are installed by default for every
Elasticsearch and OpenSearch version. Since both services run as containers, additional plugins are installed by
executing the plugin binary inside the running service container, and the container needs to be restarted
afterwards for the change to take effect (e.g. `valet.sh service restart elasticsearch7`).

elasticsearch/opensearch plugin installation on Ubuntu (via `podman exec`)
```bash
# elasticsearch 1
podman exec vsh-elasticsearch1 /usr/share/elasticsearch/bin/plugin install <pluginname>

# elasticsearch 2
podman exec vsh-elasticsearch2 /usr/share/elasticsearch/bin/plugin install <pluginname>

# elasticsearch 5
podman exec vsh-elasticsearch5 /usr/share/elasticsearch/bin/elasticsearch-plugin install <pluginname>

# elasticsearch 6
podman exec vsh-elasticsearch6 /usr/share/elasticsearch/bin/elasticsearch-plugin install <pluginname>

# elasticsearch 7
podman exec vsh-elasticsearch7 /usr/share/elasticsearch/bin/elasticsearch-plugin install <pluginname>

# elasticsearch 8
podman exec vsh-elasticsearch8 /usr/share/elasticsearch/bin/elasticsearch-plugin install <pluginname>

# opensearch 1
podman exec vsh-opensearch1 /usr/share/opensearch/bin/opensearch-plugin install <pluginname>

# opensearch 2
podman exec vsh-opensearch2 /usr/share/opensearch/bin/opensearch-plugin install <pluginname>

# opensearch 3
podman exec vsh-opensearch3 /usr/share/opensearch/bin/opensearch-plugin install <pluginname>
```


elasticsearch/opensearch plugin installation on macOS (via `container exec`)
```bash
# elasticsearch 1
container exec --user root vsh-elasticsearch1 /usr/share/elasticsearch/bin/plugin install <pluginname>

# elasticsearch 2
container exec --user root vsh-elasticsearch2 /usr/share/elasticsearch/bin/plugin install <pluginname>

# elasticsearch 5
container exec --user root vsh-elasticsearch5 /usr/share/elasticsearch/bin/elasticsearch-plugin install <pluginname>

# elasticsearch 6
container exec --user root vsh-elasticsearch6 /usr/share/elasticsearch/bin/elasticsearch-plugin install <pluginname>

# elasticsearch 7
container exec --user root vsh-elasticsearch7 /usr/share/elasticsearch/bin/elasticsearch-plugin install <pluginname>

# elasticsearch 8
container exec --user root vsh-elasticsearch8 /usr/share/elasticsearch/bin/elasticsearch-plugin install <pluginname>

# opensearch 1
container exec --user root vsh-opensearch1 /usr/share/opensearch/bin/opensearch-plugin install <pluginname>

# opensearch 2
container exec --user root vsh-opensearch2 /usr/share/opensearch/bin/opensearch-plugin install <pluginname>

# opensearch 3
container exec --user root vsh-opensearch3 /usr/share/opensearch/bin/opensearch-plugin install <pluginname>
```
