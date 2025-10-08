---
hide:
- footer
---

# ElasticSearch

## Version

Version 1,2,5,6,7 and 8 of Elasticsearch and Version 1,2 and 3 of OpenSearch will be installed on your host. You can use each version at the same time, because different TCP ports are used.

|Elasticsearch version|TCP port|running by default|
|-------------|--------|-------|
|1.x|9201|NO|
|2.x|9202|NO|
|5.x|9205|NO|
|6.x|9206|YES|
|7.x|9207|NO|
|8.x|9208|NO|


| OpenSearch version | TCP port |running by default|
|--------------------|----------|-------|
| 1.x                | 9221     |NO|
| 2.x                | 9222     |NO|
| 3.x                | 9223     |NO|


!!! Info
    The default Elasticsearch can also be accessed via TCP port 9200!

## manage Elasticsearch services

Only Elasticsearch 6 is running by default to reduce overall load and memory consumption. You can start/stop and enable/disable each elasticsearch version via valet.sh.

```bash
# stop and disable elasticsearch 5
valet.sh service disable elasticsearch5
 
# start and enable elasticsearch 5
valet.sh service enable elasticsearch5
```

!!! Warning
    You are able to start/stop a service via systemd (Ubuntu) or launchctl (macOS), but you might face some issues when running the "valet.sh install" command.

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

