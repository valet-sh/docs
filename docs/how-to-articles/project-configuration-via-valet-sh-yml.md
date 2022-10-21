---
hide:
- footer
---

# Project configuration via .valet-sh.yml

Create a stub file
------------------

To create a stub file execute the following command

```bash
valet.sh init
```

This creates the file `.valet-sh.yml` in the current folder, thus make sure to have your project root as current working directory when executing this command.

After having created the stub file, make sure to configure the settings as required for your project.

The documentation for the command above can be found [here](https://valet.sh/display/VSH/init).

Configuration settings
----------------------

WIP: this list may not be completely finished.

| Configuration Path                                                        | Example                                                                                                                                  | Default                                                          | Description                                                                                                                                                                                                                                                                                                                                                                                            |
|---------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| hub                                                                       |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| hub &gt; host                                                             | xyz.yourserver.com                                                                                                                       | dummy.example.com                                                | SFTP Server to fetch instance backup files from                                                                                                                                                                                                                                                                                                                                                        |
| hub &gt; port                                                             | 22                                                                                                                                       | 22                                                               | SFTP Port                                                                                                                                                                                                                                                                                                                                                                                              |
| hub &gt; path                                                             | /data                                                                                                                                    | /data                                                            | Absolute path in which instance backup files are provided                                                                                                                                                                                                                                                                                                                                              |
| hub &gt; user                                                             | root                                                                                                                                     |                                                                  | SFTP User                                                                                                                                                                                                                                                                                                                                                                                              |
| services                                                                  |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| services &gt; composer                                                    |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| services &gt; composer &gt; version                                       | 2                                                                                                                                        | 1                                                                | Composer version to be used inside the project (1 or 2).                                                                                                                                                                                                                                                                                                                                               |
| services &gt; node                                                        |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| services &gt; node &gt; version                                           | 11                                                                                                                                       | 14                                                               | Node.js version that shall be used to set up the project                                                                                                                                                                                                                                                                                                                                               |
| services &gt; php                                                         |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| services &gt; php &gt; version                                            |                                                                                                                                          | 7.4                                                              | The PHP version for the project. This value will ensure:The given version is used for web access to your project (e. g. project.test)The given version is used on the CLI within the project folder                                                                                                                                                                                                    |
| services &gt; mysql                                                       |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| services &gt; mysql &gt; version                                          |                                                                                                                                          | 8.0                                                              | The MySQL version for the project. The given version will be started and the dump will be imported into this instance.                                                                                                                                                                                                                                                                                 |
| services &gt; mysql &gt; database                                         |                                                                                                                                          | projectx                                                         | Database name to import the dump. If the database already exists, it will be dropped before.                                                                                                                                                                                                                                                                                                           |
| services &gt; mariadb                                                     |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| services &gt; mariadb &gt; version                                        |                                                                                                                                          | 10.4                                                             | The MariaDB version for the project. The given version will be started and the dump will be imported into this instance.                                                                                                                                                                                                                                                                               |
| services &gt; mariadb &gt; database                                       |                                                                                                                                          | projectx                                                         | Database name to import the dump. If the database already exists, it will be dropped before.                                                                                                                                                                                                                                                                                                           |
| services &gt; elasticsearch                                               |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| services &gt; elasticsearch &gt; version                                  | 6                                                                                                                                        | 7                                                                | The Elasticsearch version for the project.                                                                                                                                                                                                                                                                                                                                                             |
| services &gt; elasticsearch &gt; plugins                                  |                                                                                                                                          | `analysis-phonetic` and `analysis-icu                            | Subset of plugins to enable, specified in YAML block sequence notation.                                                                                                                                                                                                                                                                                                                                |
| services &gt; rabbitmq                                                    |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| services &gt; rabbitmq &gt; vhost                                         |                                                                                                                                          | project-x                                                        | Name of the RabbitMQ virtual host that will be used in the project. If the vhost does not exist, it is created                                                                                                                                                                                                                                                                                         |
| instance                                                                  |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| instance &gt; key                                                         |                                                                                                                                          | projectX                                                         | The 2nd level domain used to access the project locally.Example:Given that the value "myproject" is configured, the project will be accessible via the domain "myproject.test"                                                                                                                                                                                                                         |
| instance &gt; type                                                        |                                                                                                                                          | magento2                                                         | Defines the project type, which will be used when linking the project.Valid values are:"magento1""magento2""neos"""                                                                                                                                                                                                                                                                                    |
| instance &gt; path                                                        |                                                                                                                                          | src                                                              | Defines the path, relative to the project root, to the document root of the project.                                                                                                                                                                                                                                                                                                                   |
| instance &gt; multidomain                                                 |                                                                                                                                          | de: "default"<br>  en: "en"                                      | Defines the mapping of domain prefixes (aka 3rd level domains) to store codes, specified as YAML Mapping of Scalars.Example:Given thatthe project is accessible locally using the domain "myproject.test"there is a store view with the store code "foo_bar"the store view shall be accessible through the domain "myfoo.myproject.test"Then the following mapping entry should be addedmyfoo: foo_bar |
| instance &gt; sync                                                        |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| instance &gt; sync &gt; identifier                                        | prod                                                                                                                                     | test                                                             | Defines the unique name of the remote instance from which data (database &amp; files) shall be copied when restoring.                                                                                                                                                                                                                                                                                  |
| instance &gt; sync &gt; db                                                | false                                                                                                                                    | true                                                             | Not in use yet                                                                                                                                                                                                                                                                                                                                                                                         |
| instance &gt; sync &gt; fs                                                |                                                                                                                                          | `pub/media                                                       | Defines the paths, relative to&nbsp;instance &gt; path&nbsp; that shall be copied from the remote instance when restoring.                                                                                                                                                                                                                                                                             |
| instance &gt; sync &gt; post_restore_actions &gt; indexer                 |                                                                                                                                          |                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                        |
| instance &gt; sync &gt; post_restore_actions &gt; indexer &gt; reindexAll | true                                                                                                                                     | false                                                            | Defines whether all indexes shall be rebuilt after restoring.                                                                                                                                                                                                                                                                                                                                          |
| instance &gt; sync &gt; post_restore_actions &gt; indexer &gt; reindex    |                                                                                                                                          | `elasticsuite_categories_fulltext` <br> `elasticsuite_thesaurus` | Defines the indexes that shall be rebuilt after restoring.                                                                                                                                                                                                                                                                                                                                             |
| instance &gt; sync &gt; post_restore_actions &gt; commands                | `bin/test`                                                                                                                               |                                                                  | Defines commands that are executed after restoring (will be executed in instance:path folder [src]).                                                                                                                                                                                                                                                                                                   |
| instance &gt; sync &gt; post_restore_actions &gt;&nbsp;sql_queries        | `UPDATE test SET a = 1                                                                                                                   |                                                                  | Defines SQL queries that are executed after restoring.                                                                                                                                                                                                                                                                                                                                                 |
| instance &gt; crypt_key                                                   |                                                                                                                                          |                                                                  | Defines the encryption key that will be written to&nbsp;app/etc/env.php&nbsp;when initializing the instance.                                                                                                                                                                                                                                                                                           |
| instance &gt; config &gt; system                                          |                                                                                                                                          | {}                                                               | Defines scoped configuration entries that will be written to&nbsp;app/etc/env.php&nbsp;when initializing the instance.See below for supported scopes.                                                                                                                                                                                                                                                  |
| instance &gt; config &gt; system &gt; default                             | catalog:  search:    engine: elasticsearch7    elasticsearch7_server_hostname: 127.0.0.1    elasticsearch7_server_port: 9207 |                                                                  | Defines a collection of arbitrary configurations that will be written to the default scope of the&nbsp;app/etc/env.php.Supports a nesting depth of 3.                                                                                                                                                                                                                                                  |
| instance &gt; config &gt; system &gt; stores                              | see above                                                                                                                                |                                                                  | Defines a collection of arbitrary configurations that will be written to the stores scope of the&nbsp;app/etc/env.php.Supports a nesting depth of 3.                                                                                                                                                                                                                                                   |
| instance &gt; config &gt; system &gt; websites                            | see above                                                                                                                                |                                                                  | Defines a collection of arbitrary configurations that will be written to the websites scope of the&nbsp;app/etc/env.php.Supports a nesting depth of 3.                                                                                                                                                                                                                                                 |


Set up your project
-------------------

To set up your project (aka initialize your instance) using an existing `.valet-sh.yml`, execute the following command

```bash
valet.sh init-instance
```



The documentation for this command can be found [here](https://valet.sh/display/VSH/init-instance).