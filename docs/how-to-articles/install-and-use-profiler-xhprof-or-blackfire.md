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

* Execute profiled code with XHPROF_ENABLE parameter (Example: https://myproject.test/en_us/imprint?XHPROF_ENABLE=1)
* Open https://xhprof.test/ to show the results (the result dumps are stored under /var/tmp/*.xhprof)


## Blackfire

### Install Agent via Homebrew

```bash
brew tap blackfireio/homebrew-blackfire
brew install blackfire-agent
```

### Installation

```bash
curl https://packages.blackfire.io/binaries/blackfire-php/1.58.0/blackfire-php-darwin_amd64-php-74.so -o blackfire.so
sudo cp blackfire.so /usr/local/Cellar/vsh-php74/7.4.*/lib/vsh-php74/20*/
rm blackfire.so
sudo echo "extension=blackfire.so" > /usr/local/etc/vsh-php74/conf.d/ext-blackfire.ini
valet.sh service restart php74
```

### Configure


* Setup *[your account](https://blackfire.io/my/settings/credentials)*
* Configure the server ID with
```bash
blackfire-agent -register
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.blackfire-agent.plist
launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.blackfire-agent.plist
Install the Chrome extension
```
* Install the *[Chrome extension](https://chrome.google.com/webstore/detail/blackfire-profiler/miefikpgahefdbcgoiicnmpbeeomffld)*


### Usage
Click the profile button (of the Chrome extension) on a webpage using the PHP version Blackfire has been enabled for.