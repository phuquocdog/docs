# Binance Smart Chain Fullnode

## Fullnodes Functions <a id="fullnodes-functions"></a>

* Stores the full blockchain history on disk and can answer the data request from the network.
* Receives and validates the new blocks and transactions.
* Verifies the states of every accounts.

## Supported Platforms <a id="supported-platforms"></a>

We support running a full node on `Mac OS X`and `Linux`.

## Minimum Requirements <a id="minimum-requirements"></a>

The hardware must meet certain requirements to run a full node.

* VPS running recent versions of Mac OS X or Linux.
* 500 GB of free disk space
* 4 cores of CPU and 8 gigabytes of memory \(RAM\).
* A broadband Internet connection with upload/download speeds of at least 1 megabyte per second

## Settings <a id="settings"></a>

### Sync Mode <a id="sync-mode"></a>

* Fast Sync

The **default** sync mode. Synchronizes a full node doing a fast synchronization by downloading the entire state database, requesting the headers first, and filling in block bodies and receipts afterward. Once the fast sync reaches the best block of the Binance Smart Chain network, it switches to full sync mode.

* Full Sync

Synchronizes a full node starting at genesis, verifying all blocks and executing all transactions. This mode is a bit slower than the fast sync mode but comes with increased security.

## Steps to Run a Fullnode <a id="steps-to-run-a-fullnode"></a>

1.Build from source code

Make sure that you have installed [Go 1.13+](https://golang.org/doc/install) and have added `GOPATH` to `PATH` environment variable

```text
git clone https://github.com/binance-chain/bsc
# Enter the folder clv was cloned into
cd clv
# Comile and install clv
make geth
```

or you can download the pre-build binaries from [release page](https://github.com/binance-chain/bsc/releases/latest) or follow the instructions below:

```text
# Linux
wget --no-check-certificate https://github.com/binance-chain/bsc/releases/download/v1.0.2/geth_linux
# MacOS
wget --no-check-certificate https://github.com/binance-chain/bsc/releases/download/v1.0.2/geth_mac
```

2.Download the config files

Download `genesis.json` and `config.toml` by:

```text
## mainet
wget --no-check-certificate  $(curl -s https://api.github.com/repos/binance-chain/bsc/releases/latest |grep browser_ |grep mainnet |cut -d\" -f4)
unzip mainnet.zip

## testnet
wget --no-check-certificate  $(curl -s https://api.github.com/repos/binance-chain/bsc/releases/latest |grep browser_ |grep testnet |cut -d\" -f4)
unzip testnet.zip
```

3.Write genesis state locally

```text
geth --datadir node init genesis.json
```

You could see the following output:

```text
INFO [05-19|14:53:17.468] Allocated cache and file handles         database=/Users/huangsuyu/Downloads/clv/node/geth/chaindata cache=16.00MiB handles=16
INFO [05-19|14:53:17.498] Writing custom genesis block
INFO [05-19|14:53:17.501] Persisted trie from memory database      nodes=21 size=56.84KiB time=357.915µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=-574.00B
INFO [05-19|14:53:17.502] Successfully wrote genesis state         database=chaindata hash=7d79cc…fb0d1e
INFO [05-19|14:53:17.503] Allocated cache and file handles         database=/Users/huangsuyu/Downloads/clv/node/geth/lightchaindata cache=16.00MiB handles=16
INFO [05-19|14:53:17.524] Writing custom genesis block
INFO [05-19|14:53:17.525] Persisted trie from memory database      nodes=21 size=56.84KiB time=638.396µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=-574.00B
INFO [05-19|14:53:17.528] Successfully wrote genesis state         database=lightchaindata hash=7d79cc…fb0d1e
```

4.Start your fullnode or a validator node

```text
## start a full node
geth --config ./config.toml --datadir ./node --pprofaddr 0.0.0.0 --metrics --pprof
```

start a validator node

```text
## generate the consensus key and input the password
geth account new --datadir ./node
echo {your-password} > password.txt
geth --config ./config.toml --datadir ./node -unlock {your-validator-address} --password password.txt  --mine --allow-insecure-unlock  --pprofaddr 0.0.0.0 --metrics --pprof
```

5.Monitor node status

you can monitor the log from `/node/clv.log` by default.

