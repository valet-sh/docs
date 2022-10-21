---
hide:
- footer
---

# NodeJS

## Versions

nodeJs is preinstalled by `valet.sh install`. However, you can switch to any version via the `nvm` version manager.

## Switch version
To change the Node.js version in your current terminal, just execute the following command.

Change nodejs to the latest 11.* release
```bash
#<version> can be a major version like 6, 8, 10, 11,15 or a specific release like "8.16.2"
nvm install <version>

Example:
nvm install 11
```

## Set a default Version

nvm only changes the Node.js version for your current terminal window. To set a new default version for your system execute the following command with your desired version

Set a specific node version as system default
```bash
#<version> can be a major version like 6, 8, 10, 11,15 or a specific release like "8.16.2"
nvm alias default <version>
 
Example:
nvm alias default 11
```


## Package-Manger

nodejs comes with the `node-package-manager` or `npm`. npm and all installed global npm packages are bound to the installed nodejs version release. For instance when you install the npm package "yarn" globally ("npm install -g yarn") its only available as long as you use the same nodejs version. After switching from e.g. node 11 to node 15 you have to install `yarn` again (by the same command). 

