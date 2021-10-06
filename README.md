# Recommended way to install truffle on a Linux or MacOS System
If you're running Truffle on Linux or MacOS, you should not install it with sudo, otherwise you might encounter some permission issues. It is recommended to install truffle as a normal user. Before we can install truffle as a normal user we have to cleanup the system. It is also recommended to install nodejs and npm with nvm (node version manager). An advantage of nvm is that you can run different node versions on the same machine.

## Cleanup node and npm
### Remove all packages which have been installed with `sudo npm install -g`
First we want to find out which packages have been installed with `sudo npm install -g`.
Get a list of all installed packages:

`$ sudo npm list -g --depth=0`

```
/usr/lib 
|--ganache-cli@6.1.8 
|--npm@6.7.0 
+--truffle@5.0.3
```

Now we want to remove them

`$ sudo npm remove -g ganache-cli`

`$ sudo npm remove -g truffle`

`$ sudo npm remove -g npm`


If you have additional packages in the tree, you can also remove them.

## Installation of node and npm with nvm
### Install & Update Script

To **install** or **update** nvm, you should run the [install script][2]. To do that, you may either download and run the script manually, or use the following cURL or Wget command:
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

Running either of the above commands downloads a script and runs it. The script clones the nvm repository to `~/.nvm`, and attempts to add the source lines from the snippet below to the correct profile file (`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`).

<a id="profile_snippet"></a>
```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```


### Install nvm (node version manager)
See: https://github.com/creationix/nvm

`$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash`

In order to load the new environment you have to close your console and open a new one


### Install node.js with nvm
`$ nvm install node`

"node" is an alias for the latest version

### Install the latest npm version
`$ npm install -g npm`


### Delete and reset the npm prefix
See: https://stackoverflow.com/questions/34718528/nvm-is-not-compatible-with-the-npm-config-prefix-option

`$ npm config delete prefix`

`$ npm config set prefix $NVM_DIR/versions/node/v16.10.0`

## Install truffle as a normal user
`$ npm install -g truffle`

## Install ganache-cli and other packages as a normal user
`$ npm install -g ganache-cli`

Install the other packages which you had installed as sudo, such as create-react-app.

<hr>

## Linux specific instructions

### Remove node
If you installed node with a the package manager of your Linux distro you can delete the package and skip Remove node and Remove npm. If you installed it manually you have to delete it manually.

We have to find out where node is installed before we can delete it.

`$ whereis node`

in my case I get the following output

`node: /usr/bin/node /usr/share/man/man1/node.1.gz`

find the location of node_modules node and delete it

`$ sudo rm /usr/bin/node /usr/share/man/man1/node.1.gz`


### Remove npm
We have to find out where npm is installed before we can delete it.

`$ sudo whereis npm`

in my case I get the follwing output:

`npm: /usr/bin/npm /usr/share/man/man1/npm.1.gz /usr/share/man/man1/npm.1`

`$ sudo ls -l /usr/bin/npm`

`lrwxrwxrwx 1 root root 38 Feb  4 08:47 /usr/bin/npm -> ../lib/node_modules/npm/bin/npm-cli.js`

`$ sudo rm -rf /usr/bin/npm /usr/lib/node_modules/npm/bin/npm`

`$ sudo rm -rf /usr/share/man/man1/npm.1.gz /usr/share/man/man1/npm.1`

Depending on the linux distribution you might have different paths

Now that we have cleaned up everything we can start with the installation of nvm and node

## Check the installation
`$ whereis truffle`

If everything went as expected truffle should be installed in:

`~/.nvm/versions/node/v11.10.0/bin/truffle`
