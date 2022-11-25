---
hide:

- footer

---

# Install and use Profiler XHProf or Blackfire

## XHprof

### Installation module

example installation for PHP7.4

```bash
valet.sh service default php74
pecl7.4 install xhprof
valet.sh service restart php74
```

example installation for PHP8.1

```bash
valet.sh service default php81
pecl8.1 install xhprof
valet.sh service restart php81
```

### Webinterface

```bash
mkdir -p ~/Workspace/git/
cd ~/Workspace/git/
git clone https://github.com/longxinH/xhprof
cd xhprof/xhprof_html
valet.sh service enable php74
valet.sh link xhprof php74
brew install graphviz
```

Save this patch as `xhprof.patch` inside `~/Workspace/git/xhprof` and execute `git apply xhprof.patch`:

```diff
diff --git a/xhprof_html/index.php b/xhprof_html/index.php
index f21d32f..71c89e7 100644
--- a/xhprof_html/index.php
+++ b/xhprof_html/index.php
@@ -80,7 +80,7 @@ $vbbar = ' class="vbbar"';
 $vrbar = ' class="vrbar"';
 $vgbar = ' class="vgbar"';
 
-$xhprof_runs_impl = new XHProfRuns_Default();
+$xhprof_runs_impl = new XHProfRuns_Default(__DIR__.'/files');
 
 displayXHProfReport($xhprof_runs_impl, $params, $source, $run, $wts,
                     $symbol, $sort, $run1, $run2);
diff --git a/xhprof_lib/utils/xhprof_lib.php b/xhprof_lib/utils/xhprof_lib.php
index 507e669..4067391 100644
--- a/xhprof_lib/utils/xhprof_lib.php
+++ b/xhprof_lib/utils/xhprof_lib.php
@@ -908,7 +908,7 @@ function xhprof_param_init($params) {
     }
 
     if ($k === 'run') {
-      $p = implode(',', array_filter(explode(',', $p), 'ctype_xdigit'));
+      #$p = implode(',', array_filter(explode(',', $p), 'ctype_xdigit'));
     }
 
     if ($k == 'symbol') {
```

### Usage

```php
<?php
 
// check if we need to profile this page using xhprof
$useXhprof = isset($_GET['XHPROF_ENABLE']);
 
// enable xhprof
if ($useXhprof) {
    xhprof_enable();
}
 
... your code to profile ...
 
// disable xhprof and save profile file
if ($useXhprof) {
    file_put_contents(
        sys_get_temp_dir() . DIRECTORY_SEPARATOR .
        sprintf(
            'profiling_%s_%s.%s.xhprof',
            date('Y-m-d-His'),
            trim(preg_replace('/[^a-z0-9]/i', '_', explode('?', $_SERVER['REQUEST_URI'])[0]), '_'),
            trim(preg_replace('/[^a-z0-9]/i', '_', $_SERVER['HTTP_HOST']), '_')
        ),
        serialize(xhprof_disable())
    );
}
```

* Ensure `/usr/local/etc/vsh-php81/conf.d/ext-blackfire.ini` does not exist or is commented out and restart
  PHP `valet.sh service restart all`
* Execute profiled code with `XHPROF_ENABLE` parameter (Example: https://myproject.test/en_us/imprint?XHPROF_ENABLE=1)
* Open https://xhprof.test/ to show the results (the result dumps are stored under `/var/tmp/*.xhprof`
  / `~/Workspace/git/xhprof/xhprof_html/files/*.xhprof`)

## Blackfire

### Install Agent via Homebrew

```bash
brew tap blackfireio/homebrew-blackfire
brew install blackfire-agent
```

### Installation

See [this url](https://blackfire.io/docs/up-and-running/installation?action=install&mode=full&location=local&os=manual&language=php&agent=23d91fab-ddee-4d1c-b260-f367622b166c&version=latest&forced_os=darwin)
.

Example for PHP7.4

```bash
curl https://packages.blackfire.io/binaries/blackfire-php/1.58.0/blackfire-php-darwin_amd64-php-74.so -o blackfire.so
sudo cp blackfire.so /usr/local/Cellar/vsh-php74/7.4.*/lib/vsh-php74/20*/
rm blackfire.so
sudo echo "extension=blackfire.so" > /usr/local/etc/vsh-php74/conf.d/ext-blackfire.ini
valet.sh service restart php74
```

Example for PHP8.1

```bash
curl https://packages.blackfire.io/binaries/blackfire-php/1.85.0/blackfire-php-darwin_amd64-php-81.so -o blackfire.so
sudo cp blackfire.so /usr/local/Cellar/vsh-php81/8.1.*/lib/vsh-php81/20*/
rm blackfire.so
sudo echo "extension=blackfire.so" > /usr/local/etc/vsh-php81/conf.d/ext-blackfire.ini
valet.sh service restart php81
```

### Configure

* Setup *[your account](https://blackfire.io/my/settings/credentials)*
* Configure the server ID with `blackfire-agent -register`
* and restart the agent with either

```bash
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.blackfire-agent.plist
launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.blackfire-agent.plist
```

_or_

```bash
brew services restart blackfire-agent
```

* Install
  the *[Chrome extension](https://chrome.google.com/webstore/detail/blackfire-profiler/miefikpgahefdbcgoiicnmpbeeomffld)*

### Usage

Ensure `/usr/local/etc/vsh-php81/php.ini` (replace `php81` with correct PHP version) does not
contain `extension="xhprof.so"` or it is commented out and restart
PHP `valet.sh service restart all`.

Click the profile button (of the Chrome extension) on a webpage using the PHP version Blackfire has been enabled for.
