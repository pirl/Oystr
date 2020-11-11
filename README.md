# THIS REPO OF PIRL IS DEPRECIATED, WE HAVE MOVED TO NPOS PROTOCOL


# Oystr

Please note that this repository is the Electron host for the Meteor based wallet dapp whose repository is located here: https://github.com/pirl/Oystr-Wallet-dApp

## Installation

If you want to install the app from a pre-built version on the [release page](https://github.com/pirl/oystr/releases),
you can simply run the executeable after download.

For updating simply download the new version and copy it over the old one (keep a backup of the old one if you want to be sure).

#### Config folder
The data folder for Oystr is stored in other places:

- Windows `%APPDATA%\Oystr`
- macOS `~/Library/Application\ Support/Oystr`
- Linux `~/.config/Oystr`


## Development

For development, a Meteor server will need to be started to assist with live reload and CSS injection.
Once a Oystr version is released the Meteor frontend part is bundled using the `meteor-build-client` npm package to create pure static files.

### Dependencies

To run Oystr in development you need:

- [Node.js](https://nodejs.org) `v7.x` (use the prefered installation method for your OS)
- [Meteor](https://www.meteor.com/install) javascript app framework
- [Yarn](https://yarnpkg.com/) package manager
- [Electron](http://electron.atom.io/) `v1.4.15` cross platform desktop app framework
- [Gulp](http://gulpjs.com/) build and automation system

Install the latter ones via:

    $ curl https://install.meteor.com/ | sh
    $ curl -o- -L https://yarnpkg.com/install.sh | bash
    $ yarn global add electron@1.4.15
    $ yarn global add gulp

### Initialisation

Now you're ready to initialise Oystr for development:

    $ git clone https://github.com/pirl/Oystr.git
    $ cd Oystr
    $ yarn

To update Oystr in the future, run:

    $ cd Oystr
    $ git pull
    $ yarn

### Run Oystr

For development we start the interface with a Meteor server for autoreload etc.
*Start the interface in a separate terminal window:*

    $ cd Oystr/interface && meteor --no-release-check

In the original window you can then start Oystr with:

    $ cd Oystr
    $ electron .

*NOTE: client-binaries (e.g. [pirl](https://github.com/pirl/pirl)) specified in [clientBinaries.json](https://github.com/pirl/Oystr/blob/master/clientBinaries.json) will be checked during every startup and downloaded if out-of-date, binaries are stored in the [config folder](#config-folder)*

*NOTE: use `--help` to display available options, e.g. `--loglevel debug` (or `trace`) for verbose output*

### Run the Wallet

Start the wallet app for development, *in a separate terminal window:*

    $ cd Oystr/interface && meteor --no-release-check

    // and in another terminal

    $ cd my/path/Oystr-Wallet-dApp/app && meteor --port 3050

In the original window you can then start Oystr using wallet mode:

    $ cd Oystr
    $ electron . --mode wallet


### Connecting to node via HTTP instead of IPC

This is useful if you have a node running on another machine, though note that
it's less secure than using the default IPC method.

```bash
$ electron . --rpc http://localhost:8545
```


### Passing options to Pirl

You can pass command-line options directly to Pirl by prefixing them with `--node-` in
the command-line invocation:

```bash
$ electron . --mode Oystr --node-rpcport 19343 --node-networkid 2
```

The `--rpc` Oystr option is a special case. If you set this to an IPC socket file
path then the `--ipcpath` option automatically gets set, i.e.:

```bash
$ electron . --rpc /my/pirl.ipc
```

...is the same as doing...


```bash
$ electron . --rpc /my/pirl.ipc --node-ipcpath /my/pirl.ipc
```

### Deployment

Our build system relies on [gulp](http://gulpjs.com/) and [electron-builder](https://github.com/electron-userland/electron-builder/).

#### Dependencies

[meteor-build-client](https://github.com/frozeman/meteor-build-client) bundles the [meteor](https://www.meteor.com/)-based interface. Install it via:

    $ npm install -g meteor-build-client

Furthermore cross-platform builds require additional [`electron-builder` dependencies](https://github.com/electron-userland/electron-builder/wiki/Multi-Platform-Build#linux). On macOS those are:

    // windows deps
    $ brew install wine --without-x11 mono makensis

    // linux deps
    $ brew install gnu-tar libicns graphicsmagick xz

#### Generate packages

To generate the binaries for Oystr run:

    $ gulp

To generate the Pirl Wallet (this will pack the one Ðapp from https://github.com/pirl/Oystr-Wallet-dApp):

    $ gulp --wallet

The generated binaries will be under `dist_mist/release` or `dist_wallet/release`.


#### Options

##### platform

To build binaries for specific platforms (default: all available) use the following flags:

    // on mac
    $ gulp --win --linux --mac

    // on linux
    $ gulp --win --linux

    // on win
    $ gulp --win

##### walletSource

With the `walletSource` you can specify the Wallet branch to use, default is `master`:

    $ gulp --wallet --walletSource develop


Options are:

- `master`
- `develop`
- `local` Will try to build the wallet from [oystr/]../Oystr-Wallet-dApp/app

*Note: applicable only when combined with `--wallet`*

#### Checksums

Spits out the MD5 checksums of distributables.

It expects installer/zip files to be in the generated folders e.g. `dist_mist/release`

    $ gulp checksums [--wallet]


## Testing

Tests are ran using [Spectron](https://github.com/electron/spectron/), a webdriver.io runner built for Electron. 

First make sure to build Mist with:

    $ gulp

Then run the tests:

    $ gulp test

*Note: Integration tests are not yet supported on Windows.*
