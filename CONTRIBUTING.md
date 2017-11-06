# How to Contribute

## Issues / Bug reports

**Read the existing issues first, and also search in the closed issues. You may find yours already.**

To help make Oystr (Pirl Wallet) better please file issue with the following basic descriptions:

- What do you run? binary from [releases](https://github.com/pirl/oystr/releases) or the development version from the [commandline](https://github.com/ethereum/oystr#run-oystr)
- Which version do you used? You can find that in the `VERSION` file in the Oystr folder
- What OS you're on?
- Provide a log file if necessary, you can find that in the Oystr data folder (Linux: `~/.config/Oystr/*.log`, Windows: `%APPDATA%/Roaming/Oystr/*.log`, MacOSX: `~/Library/Application Support/Oystr/*.log`)
- Ideally also a screenshot, if its an interface issue


## Pull Requests

If you want to make a PR please make sure you add a understandable description of what it is you're adding/changing/fixing.

For formatting we use 4 *spaces* as indentation.

If you add any modules or files, please give them a module description and or a class description:

```
/**
The IPC provider backend filter and tunnel all incoming request to the IPC geth bridge.

@module ipcProviderBackend
*/

/**
Oystr API

Provides an API for all dapps, which specifically targets features from the Oystr browser

@class oystr
@constructor
*/
```

