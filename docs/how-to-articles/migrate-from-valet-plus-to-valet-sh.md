---
hide:
- footer
---

# Migrate from valet-plus to valet.sh

Please read all instructions carefully and run command by command. If you run into any errors, please report them before continuing to ensure the issue gets fixed for the next person to upgrade.

!!! Info
    Please be sure to be on a supported operating system version before continuing. See *[Support-Matrix](/getting-started/support-matrix)*.

!!! Warning
    Caution: Your MySQL databases will not be migrated.
    Please create backups for the databases you need and delete all databases before proceeding.

Ensure Command Line Tools are installed
```bash
xcode-select --install # if this fails, download and install "Command Line Tools for Xcode 12" (or whatever version your OS needs) via https://developer.apple.com/download/more/
```

Uninstall valet-plus
```bash
valet stop
composer global remove techdivision/valet-plus
rm -rf ~/.valet
rm -f /usr/local/var/log/php-fpm.log
sed -i -e 's/^conf-file=/#conf-file=/g' /usr/local/etc/dnsmasq.conf
unsetopt NOMATCH; sudo rm /Library/LaunchDaemons/homebrew.mxcl.php* 2&>1; setopt NOMATCH
```

Uninstall valet.sh 1.x
```bash
sudo launchctl unload -w /Library/LaunchDaemons/sh.valet.*
sudo rm -rf /Library/LaunchDaemons/sh.valet.*
sudo rm -rf /usr/local/valet-sh
```

Cleanup and uninstall brew packages
```bash
sudo rm -rf /usr/local/Cellar/dnsmasq
sudo rm -rf /usr/local/Cellar/nginx
sudo rm -rf /usr/local/Cellar/valet-php*
 
brew uninstall --force sleepwatcher httpd-bc mailhog nginx dnsmasq rabbitmq redis mysql@5.7 elasticsearch@2.4 elasticsearch@5.6 valet-php@5.6 valet-php@7.0 valet-php@7.1 valet-php@7.2 valet-php@7.3 valet-php@7.4
brew untap henkrehorst/homebrew-php
```

Install valet.sh
```bash
cp ~/.zshrc ~/.zshrc.bak
cp -r ~/.oh-my-zsh ~/.oh-my-zsh.bak
 
# this error can be ignored: unshallow on a complete repository does not make sense
git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core fetch --unshallow
git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask fetch --unshallow
 
brew update && brew upgrade
brew doctor
brew cleanup
 
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/valet-sh/install/master/install.sh)"
valet.sh self-upgrade
valet.sh install
```

After installation check if *(https://mailhog.test)[https://mailhog.test]* is available in your browser. Maybe you need to restart your system.


!!! Info
    Your rabbitMQ configs will remain.
    
    As your old mySQL installation is removed within the upgrade to valet.sh 2, there may still be a large data folder on your Mac. You can remove it safely by running the following command:
    rm -rf /usr/local/var/mysql
    
    If you want to use your Touch ID for sudo, see this *[stack exchange post](https://apple.stackexchange.com/a/306324)*. You can then confirm all sudo processes (and therefore also all valet.sh commands) with your Touch ID.
    
    To set up your first project see the following how to: Setup magento project
    
    Please also refer to the Migration-Cheatsheet from valet-plus to valet.sh

