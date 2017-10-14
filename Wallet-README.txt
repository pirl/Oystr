Pirl Wallet

The Pirl wallet, which allows you to create simple and multisig wallets to manage your pirl.

The wallet contains its own node, but can also use an already running one, if the IPC path of that node is the standard path.
(See below)

## Running on a testnet

When you start the wallet on a testnet (e.g. different `--datadir`) you need to make sure to set the `--ipcpath` back to the original one.

On OSX its `~/Library/Pirl/pirl.ipc` on linux `~/.ethereum/pirl.ipc` and on windows it uses a named pipe, which doesn't need to be renamed.

Example:

    $ pirl --datadir /my/chain/ --networkid 23 --ipcpath ~/Library/Pirl/pirl.ipc



### Original contract

Once you start the app while running a testnet, the wallet need to deploy an original contract,
which will be used by the wallet contracts you create.

The point of the original wallet is that wallet contract creation is cheaper,
as not the full code has to be deployed for every wallet.

You need to make sure that the account displayed for the original wallet creation is unlocked and has at least 1 pirl.


## Paths

The paths which store your wallets database and node are different:

The wallet (Oystr) stores its data at:
- Mac: ~/Library/Application Support/Oystr
- Windows: %APPDATA%\Roaming\Oystr
- Linux: ~/.config/Oystr

The nodes data is stored at:
- Mac: ~/Library/Pirl
- Windows: %APPDATA%\Roaming\Pirl
- Linux: ~/.pirl


## Issues

If you find issues or have suggestion, please report them at  
https://github.com/pirl/oystr-wallet-dapp/issues



## Repository

The wallet code can be found at   
https://github.com/pirl/oystr-wallet-dapp

And the binary application code, which wraps the wallet app can be found at   
https://github.com/pirl/oystr/


## Bundling the wallet

To bundle the binaries yourself follow the instructions on the oystr#wallet readme  
https://github.com/pirl/oystr/tree/wallet#deployment
