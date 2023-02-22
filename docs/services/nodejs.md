---
hide:
- footer
---

# NodeJS


## Version Manager

valet.sh supports the version managers [nvm](https://github.com/nvm-sh/nvm) and [volta](https://volta.sh/). It is not possible to use both at the same time.
nvm is installed by default. 

How to change the version manager:
```bash
# switch to volta
valet.sh config set default_nvm volta

# switch back to nvm
valet.sh config set default_nvm nvm
```
!!! Warning
    `valet.sh install` must be run each time to apply the change! 


## nvm usage

### Switch node versions
To change the Node.js version in your current terminal, just execute the following command.

Change nodejs to the latest 11.* release
```bash
#<version> can be a major version like 6, 8, 10, 11,15 or a specific release like "8.16.2"
nvm install <version>

Example:
nvm install 11
```

### Set a default Version

nvm only changes the Node.js version for your current terminal window. To set a new default version for your system execute the following command with your desired version

Set a specific node version as system default
```bash
#<version> can be a major version like 6, 8, 10, 11,15 or a specific release like "8.16.2"
nvm alias default <version>
 
Example:
nvm alias default 11
```

### Package-Manger

nodejs comes with the `node-package-manager` or `npm`. npm and all installed global npm packages are bound to the installed nodejs version release. For instance when you install the npm package "yarn" globally ("npm install -g yarn") its only available as long as you use the same nodejs version. After switching from e.g. node 11 to node 15 you have to install `yarn` again (by the same command). 

## volta usage

### Switch node version

The version is installed and becomes the default version in all terminals. By `pinning` the versions, an individual version can be used for each project.

```bash
#<version> can be a major version like 6, 8, 10, 11,15 or a specific release like "8.16.2"
volta install node@<version>

Example:
volta install node@14
```

### Pin node version

!!! note ""
    Volta saves the exact version of the Node engine in your package.json so you can commit your selection to git.
    From that point on, every time you run Node inside your project directory, Volta automatically switches to that same
    version of Node you chose. Similarly, all your collaborators can do the same by installing Volta on their
    development machine.

```bash
#<version> can be a major version like 6, 8, 10, 11,15 or a specific release like "8.16.2"
volta pin node@<version>

Example:
volta pin node@18
```