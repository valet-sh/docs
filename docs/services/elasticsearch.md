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

On Ubuntu, services run directly on the host and are reachable via `127.0.0.1` and their port. On macOS, services
run as Apple containers and are additionally reachable via DNS on the `vsh-services` network, using the same port.

|Elasticsearch version|Ubuntu|macOS|
|-------------|--------|--------|
|1.x|127.0.0.1:9201|vsh-elasticsearch1.vsh-services:9201|
|2.x|127.0.0.1:9202|vsh-elasticsearch2.vsh-services:9202|
|5.x|127.0.0.1:9205|vsh-elasticsearch5.vsh-services:9205|
|6.x|127.0.0.1:9206|vsh-elasticsearch6.vsh-services:9206|
|7.x|127.0.0.1:9207|vsh-elasticsearch7.vsh-services:9207|
|8.x|127.0.0.1:9208|vsh-elasticsearch8.vsh-services:9208|


| OpenSearch version | Ubuntu | macOS |
|--------------------|----------|----------|
| 1.x                | 127.0.0.1:9221 | vsh-opensearch1.vsh-services:9221 |
| 2.x                | 127.0.0.1:9222 | vsh-opensearch2.vsh-services:9222 |
| 3.x                | 127.0.0.1:9223 | vsh-opensearch3.vsh-services:9223 |


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

## Update Elasticsearch (Ubuntu only!)

We do not have any update mechanism for minor or patch level releases at this point of time. To enforce an update simply stop the daemon and remove the package directory, ``valet.sh install`` will reinstall deleted elasticsearch version. 

!!! Warning
    all data in the affected version will be lost!


Example commands for reinstalling <strong>elasticsearch 5</strong>
```bash
valet.sh service disable elasticsearch5
rm -r /usr/local/valet-sh/packages/elasticsearch5
valet.sh install
```

## Plugins

The plugins <strong>analysis-phonetic</strong> and <strong>analysis-icu</strong> are installed by default for every Elasticsearch version. More plugins can be installed by the default plugin install executable.

elasticsearch pugin installation on Ubuntu
```bash
# elasticsearch 1
/usr/local/valet-sh/packages/elasticsearch1/bin/plugin install <pluginname>
 
# elasticsearch 2
/usr/local/valet-sh/packages/elasticsearch2/bin/plugin install <pluginname>
 
# elasticsearch 5
/usr/local/valet-sh/packages/elasticsearch5/bin/elasticsearch-plugin install <pluginname>
 
# elasticsearch 6
/usr/local/valet-sh/packages/elasticsearch6/bin/elasticsearch-plugin install <pluginname>
 
# elasticsearch 7
/usr/local/valet-sh/packages/elasticsearch7/bin/elasticsearch-plugin install <pluginname>
 
# elasticsearch 8
/usr/local/valet-sh/packages/elasticsearch8/bin/elasticsearch-plugin install <pluginname>
 
# opensearch 1
/usr/local/valet-sh/packages/opensearch1/bin/opensearch-plugin install <pluginname>

# opensearch 2
/usr/local/valet-sh/packages/opensearch2/bin/opensearch-plugin install <pluginname>
```


elasticsearch pugin installation on MacOS
```bash
# elasticsearch 1
/usr/local/opt/vsh-elasticsearch1/libexec/bin/plugin install <pluginname>
 
# elasticsearch 2
/usr/local/opt/vsh-elasticsearch2/libexec/bin/plugin install <pluginname>
 
# elasticsearch 5
/usr/local/opt/vsh-elasticsearch5/libexec/bin/elasticsearch-plugin install <pluginname>
 
# elasticsearch 6
/usr/local/opt/vsh-elasticsearch6/libexec/bin/elasticsearch-plugin install <pluginname>
 
# elasticsearch 7
/usr/local/opt/vsh-elasticsearch7/libexec/bin/elasticsearch-plugin install <pluginname>
 
# elasticsearch 8
/usr/local/opt/vsh-elasticsearch8/libexec/bin/elasticsearch-plugin install <pluginname>
 
# opensearch 1
/usr/local/opt/vsh-opensearch1/libexec/bin/opensearch-plugin install <pluginname>

# opensearch 2
/usr/local/opt/vsh-opensearch2/libexec/bin/opensearch-plugin install <pluginname>
```

