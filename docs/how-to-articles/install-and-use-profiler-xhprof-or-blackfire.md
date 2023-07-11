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
brew install blackfire
```

### Install PHP Probe

See [this url](https://blackfire.io/docs/up-and-running/installation?action=install&mode=full&version=latest&mode=full&location=local&os=manual&language=php)
.

Example for PHP7.4

```bash
curl https://packages.blackfire.io/binaries/blackfire-php/1.88.1/blackfire-php-darwin_amd64-php-74.so -o blackfire.so
sudo cp blackfire.so /usr/local/Cellar/vsh-php74/7.4.*/lib/vsh-php74/20*/
rm blackfire.so
mkdir -p /usr/local/var/run/
valet.sh service restart php74
```

Example for PHP8.1

```bash
curl https://packages.blackfire.io/binaries/blackfire-php/1.85.0/blackfire-php-darwin_amd64-php-81.so -o blackfire.so
sudo cp blackfire.so /usr/local/Cellar/vsh-php81/8.1.*/lib/vsh-php81/20*/
rm blackfire.so
mkdir -p /usr/local/var/run/
valet.sh service restart php81
```

### Add config file

Create file `/usr/local/etc/vsh-php74/conf.d/ext-blackfire.ini` with content

```editorconfig
[blackfire]
extension = blackfire.so
blackfire.server_id = xxx
blackfire.server_token = xxx

; Log verbosity level:
;   4: debug
;   3: info
;   2: warning;
;   1: error
blackfire.log_level = 2

; Log file (STDERR by default)
;blackfire.log_file = /tmp/blackfire.log

; Sets the socket where the agent is listening.
; Possible value can be a unix socket or a TCP address.
; Defaults values are:
;   - Linux: unix:///var/run/blackfire/agent.sock
;   - macOS amd64: unix:///usr/local/var/run/blackfire-agent.sock
;   - macOS arm64 (M1): unix:///opt/homebrew/var/run/blackfire-agent.sock
;   - Windows: tcp://127.0.0.1:8307
blackfire.agent_socket = unix:///opt/homebrew/var/run/blackfire-agent.sock

; Enables Blackfire Monitoring
; Enabled by default since version 1.61.0
;blackfire.apm_enabled = 1
```

### Configure

* Set up *[your account](https://blackfire.io/my/settings/credentials)*
* Configure the server ID with `blackfire agent:config --server-id=xxx --server-token=xxx`
* and restart the agent with `brew services restart blackfire`

* Install
  the
  *[Chrome extension](https://chrome.google.com/webstore/detail/blackfire-profiler/miefikpgahefdbcgoiicnmpbeeomffld)*

### Usage

Ensure `/usr/local/etc/vsh-php81/php.ini` (replace `php81` with correct PHP version) does not
contain `extension="xhprof.so"` or it is commented out and restart
PHP `valet.sh service restart all`.

Click the profile button (of the Chrome extension) on a webpage using the PHP version Blackfire has been enabled for.
