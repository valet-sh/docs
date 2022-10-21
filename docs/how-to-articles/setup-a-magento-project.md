---
hide:
- footer
---

# Setup a magento project

Go to workspace directory:
```bash
cd ~/Workspace/<PROJECT_NAME>
```

Link project via:
```bash
valet.sh link <PROJECT_NAME> php73
```

Import your database via:
```bash
valet.sh db import tmp/latest.sql.gz <PROJECT_NAME>
```

Do the project relevant settings for e.g. magento:

Edit env.php:
* change database host <strong>localhost</strong> to <strong>127.0.0.1</strong>
* change database port <strong>3306</strong> to <strong>3307</strong> for <strong>mysql5.7</strong> or <strong>3308</strong> for <strong>mysql8.0</strong> usage

Update Magento config, cache and index
```bash
bin/magento app:config:import -n
bin/magento c:f
bin/magento index:reindex
```

To install magento, you can use these commands:
```bash
COMPOSER_MEMORY_LIMIT=-1 composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition=2.3.5-p2 demo23
 
bin/magento setup:install --admin-firstname Demo --admin-lastname Demo --admin-email magento@techdivision.com --admin-user admin --admin-password admin --base-url https://demo23.test/ --db-host 127.0.0.1 --db-name demo23 --db-user root --db-password root --use-rewrites 1 --backend-frontname admin --currency EUR --timezone Europe/Berlin
```