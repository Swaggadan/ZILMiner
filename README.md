# zilminer

> Zilliqa miner with OpenCL and CUDA support. It supports both Ubuntu and Windows OS.

**zilminer** is an Ethash GPU mining worker that support Zilliqa's Proof-of-Work process. 

This project is a fork of [ethminer](https://github.com/ethereum-mining/ethminer). Please do see [ethminer README](ethminer.README.md) for more details.

## Features

* Zilliqa Getwork protocol
* Dual-Mining support
* All ethminer features


## Install

Standalone **executables** for *Linux*, *macOS* and *Windows* are provided in
the [**Releases**](https://github.com/DurianStallSingapore/ZILMiner/releases) section.
Download an archive for your operating system and unpack the content to a place
accessible from command line. After which, the zilminer will be ready to go.


## Usage

The **zilminer** is a command line program. This means you will have to launch it either
from a Windows command prompt or Linux Bash console. You can also create shortcuts to
predefined commands using a Linux Bash script or Windows batch/cmd file.
For the full list of available commands, please enter the following:

```sh
zilminer --help
```

## Settings on zilminer client

Key in the following command in your command prompt:
```sh
zilminer -P zil://wallet_address.worker_name@zil_node_ip:get_work_port
```
> Please change the *wallet_address*, *worker_name*, *zil_node_ip*, and *get_work_port* accodingly.

* For `wallet_address`: You can use the [Zilliqa Wallet](https://wallet.zilliqa.com/) to create a new keypair and a Zilliqa address.
* For `worker_name` You can key in any abitrary worker name you desire.
* For `zil_node_ip`: Please key in the IP address of the Zilliqa node.
* For `get_work_port`: Please key in the port used in `GETWORK_SERVER_PORT`. Default is `4202`.

## Dual Mining

1. Write 2 scripts yourself to start/stop other coin's miner. 
2. Add arg `--pow-start` to stop other miner before ZIL PoW starting.
3. Add arg `--pow-end` to start other miner after ZIL PoW stopped.

example:
```sh
zilminer --pow-start stopAE.bat --pow-end startAE.bat -P zil://wallet_address.worker_name@zil_node_ip:get_work_port
```

4. [Optional] If your GPU memory is not enough, add arg `--clear-dag` to clear ZIL DAG after ZIL PoW stopped.

## Dual Mining Scripts:

### Zilminer + GMiner - Beam + ZIL

Write 2 batch files:
`start_beam.bat` batch file to start beam miner:
```bat
taskkill /f /im miner.exe >null
START cmd /c "miner.exe --algo 150_5 --server beam-us.leafpool.com --port 4444 --ssl 1 --user walletxxx.namexxx"
```

`stop_beam.bat` batch file to stop beam miner:
```bat
taskkill /f /im miner.exe >null
```

Zilminer:
```bat
zilminer.exe --pow-start stop_beam.bat --pow-end start_beam.bat --pow-end-at-startup -P zil://wallet_address.worker_name@proxy.getzil.com:5000/api
```

If your GPU memory is not enghou for 2 miners, add zilminer arg `--clear-dag`

## Build

### Building from source

See [docs/BUILD.md](docs/BUILD.md) for build/compilation details.
