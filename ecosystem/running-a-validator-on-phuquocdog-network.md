# Running a validator on Phu Quoc Dog Network

This guide will instruct you on how to set up a Phu Quoc Doge validator node on Phu Quoc Dog networks (Testnet/Mainnet).

## 👉 Must Read Before Start.

Running a validator is a serious thing, you have a lot of responsibility for the staked tokens of you and nominators. You take the risk of losing your staked tokens as a slash might happen if your validator node is not properly configured. Please make sure you or your team have the necessary knowledge to run a validator node.

[Polkadot Wiki ](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-validate-polkadot)has an awesome introduction of running a validator node on the [Polkadot network](https://polkadot.network). As a member of the Polkadot ecosystem, Phu Quoc Dog follows a similar process to run and setup a validator node. We may skip some basics steps in this tutorial.

## 🛠 Hardware Requirements

* **CPU** - Recent released high end cpu, e.g. Intel 10700/Amd 5800X.
* **Memory** - 32GB for Testnet, 64GB for Sakura and Mainnet.
* **Storage** - 300GB SSD, Storage usage could increase by time, you might need to increase the capacity as the chain data grows..
* **OS**: Linux, Debian/Ubuntu LTS distributions are recommended.

## 🔧 Prepare Environment

Once you choose your cloud service provider and set-up your new server, the first thing you will do is install the necessary dependencies.

```bash
sudo apt install make clang pkg-config libssl-dev build-essential curl git
```

If you intend to build from source you need to install Rust first.

If you have already installed Rust, run the following command to make sure you are using the latest version.

```
rustup update
```

If not, this command will fetch the latest version of Rust and install it.

```
curl https://sh.rustup.rs -sSf | sh -s -- -y
```

Add the required toolchains with rustup

```
source $HOME/.cargo/env
rustup toolchain add nightly-2021-05-11
rustup target add wasm32-unknown-unknown --toolchain nightly-2021-05-11
rustup target add x86_64-unknown-linux-gnu --toolchain nightly-2021-05-11

```

Verify your installation.

```
rustc --version
```

Note - if you are using OSX and you have Homebrew installed, you can issue the following equivalent command INSTEAD of the previous one:

```
brew install cmake pkg-config openssl git llvm
```

####

#### Install & Configure Network Time Protocol (NTP) Client

[NTP](https://en.wikipedia.org/wiki/Network\_Time\_Protocol) is a networking protocol designed to synchronize the clocks of computers over a network. NTP allows you to synchronize the clocks of all the systems within the network. Currently it is required that validators' local clocks stay reasonably in sync, so you should be running NTP or a similar service. You can check whether you have the NTP client by running:

If you are using Ubuntu 18.04 / 20.04, NTP Client should be installed by default.

```
timedatectl
```

If NTP is installed and running, you should see `System clock synchronized: yes` or a similar message. If you do not see it, you can install it by executing:

```
sudo apt-get install ntp
```

ntpd will be started automatically after install. You can query ntpd for status information to verify that everything is working:

```
sudo ntpq -p
```

## ⚙ Setup PhuQuoc Doge Validator Node

Currently, we only have **PhuQuoc Doge Testnet**(**Quarks**) and **Phu Quoc Dog Mainnet**(Bosons) launched. Phu Quoc Dog Testnet opens for validators to join. _Phu Quoc Doge Mainnet operates in the NPOS mode and maintained by 6 nodes belongs to the Phu Quoc Dog Foundation_.

Validator Configuration for Phu Quoc Dog Mainnet will be updated later once it's ready for staking and validators can join.

**Build from source**

To build the `Phuquocdog` binary from the [Node](https://github.com/phuquoc/node) repository on GitHub using the source code available in the 1.0.1 release.

```
git clone https://github.com/phuquocdog/node.git
cd node
```

Build native code with the cargo release profile.

```
cargo build --release
```

This step will take a while (generally 10 - 40 minutes, depending on your hardware).

**Using a prebuilt**

If you don't want to build the binary from the source and simply prefer to download it, use the following command. Then continue at Synchronize Chain Data&#x20;

```
curl -O -L -o phuquocdog-node https://portal.phuquoc.dog/binary/phuquocdog-node
```

If your server running on ARM you need to download the file below

```
curl -O -L -o phuquocdog-node https://portal.phuquoc.dog/binary/phuquocdog-node-arm
```

#### Synchronize Chain Data

Download `phuquocdog.json` file for the Phuquocdog mainnet

```
cd $HOME
curl -O -L https://raw.githubusercontent.com/phuquocdog/node/master/node/res/phuquocdog.json
```

You can begin syncing your node by running the following commands if you do not want to start in validator mode right away:

```
chmod +x $HOME/phuquocdog-node
$HOME/phuquocdog-node --chain $HOME/phuquocdog.json --validator --rpc-cors=all --name  PQD-G01 --base-path $HOME/data
```

Then the result should be like that

```
tranduythien@pqd-g01:~$ $HOME/phuquocdog-node --chain $HOME/phuquocdog.json --validator --rpc-cors=all --bootnodes /ip4/34.209.135.220/tcp/30333/p2p/12D3KooWEc9LZpacBXG48bVVjZNUaXaQHR4qoW74Xf9tmNw1Sk4P --name  PQD-G01 --base-path $HOME/data
2021-10-06 15:20:42 Phuquocdog Node    
2021-10-06 15:20:42 ✌️  version 3.0.0-d7a4013-x86_64-linux-gnu    
2021-10-06 15:20:42 ❤️  by Phu Quoc Dog <https://phuquoc.dog>, 2017-2021    
2021-10-06 15:20:42 📋 Chain specification: Phuquocdog Main Network    
2021-10-06 15:20:42 🏷 Node name: PQD-G01    
2021-10-06 15:20:42 👤 Role: AUTHORITY    
2021-10-06 15:20:42 💾 Database: RocksDb at /home/tranduythien/data/chains/phuquocdog_main_network/db/full    
2021-10-06 15:20:42 ⛓  Native runtime: node-270 (phuquocdog-official-0.tx2.au10)    
2021-10-06 15:20:43 🔨 Initializing Genesis block/state (state: 0x4bba…5ae2, header-hash: 0xbbe6…1d84)    
2021-10-06 15:20:43 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
2021-10-06 15:20:46 ⏱  Loaded block-time = 12s from block 0xbbe65b0d6c309386a01b852ce910965607a926ac8263c640559d783539851d84    
2021-10-06 15:20:46 👶 Creating empty BABE epoch changes on what appears to be first startup.    
2021-10-06 15:20:46 🏷 Local node identity is: 12D3KooWCjogLMicHPuFwK63Cs8RUsLGKF97HeiiVhPi6aGSeWnx    
2021-10-06 15:20:46 📦 Highest known block at #0    
2021-10-06 15:20:46 〽️ Prometheus exporter started at 127.0.0.1:9615    
2021-10-06 15:20:46 Listening for new connections on 127.0.0.1:9944.    
2021-10-06 15:20:46 👶 Starting BABE Authorship worker    
2021-10-06 15:20:47 🔍 Discovered new external address for our node: /ip4/104.197.250.61/tcp/30333/p2p/12D3KooWCjogLMicHPuFwK63Cs8RUsLGKF97HeiiVhPi6aGSeWnx    
2021-10-06 15:20:51 ⚙️  Syncing, target=#5909 (2 peers), best: #2815 (0xdfda…31d9), finalized #2560 (0xc10e…8950), ⬇ 266.0kiB/s ⬆ 4.1kiB/s    
2021-10-06 15:20:53 [#3967] 🗳  creating a snapshot with metadata SolutionOrSnapshotSize { voters: 5, targets: 4 }    
2021-10-06 15:20:53 [#3967] 🗳  Starting signed phase round 1.    
2021-10-06 15:20:54 [#4267] 🗳  Starting unsigned phase round 1 enabled true.    
2021-10-06 15:20:54 [#4268] 🗳  queued unsigned solution with score [153846153846, 46461538461537, 1550343195266213964497041421]    
2021-10-06 15:20:54 [4567] 💸 new validator set of size 3 has been processed for era 1    
2021-10-06 15:20:56 💤 Idle (2 peers), best: #5731 (0xfb0c…e0b2), finalized #5632 (0x6685…972c), ⬇ 52.5kiB/s ⬆ 0.8kiB/s    
2021-10-06 15:21:01 💤 Idle (2 peers), best: #5909 (0x4ea9…8ba3), finalized #5767 (0xc2c2…48b8), ⬇ 0.5kiB/s ⬆ 0.4kiB/s    
2021-10-06 15:21:06 💤 Idle (2 peers), best: #5909 (0x4ea9…8ba3), finalized #5767 (0xc2c2…48b8), ⬇ 0.2kiB/s ⬆ 0.1kiB/s    
2021-10-06 15:21:11 💤 Idle (2 peers), best: #5909 (0x4ea9…8ba3), finalized #5767 (0xc2c2…48b8), ⬇ 0 ⬆ 0    
2021-10-06 15:21:16 💤 Idle (2 peers), best: #5909 (0x4ea9…8ba3), finalized #5767 (0xc2c2…48b8), ⬇ 0 ⬆ 0.2kiB/s    
2021-10-06 15:21:21 💤 Idle (2 peers), best: #5909 (0x4ea9…8ba3), finalized #5767 (0xc2c2…48b8), ⬇ 0.6kiB/s ⬆ 0.1kiB/s    
2021-10-06 15:21:26 💤 Idle (2 peers), best: #5909 (0x4ea9…8ba3), finalized #5767 (0xc2c2…48b8), ⬇ 0 ⬆ 0    
```

### **Running a validator as a service**

Prepare a  `phuquocdog.service`  file

```
[Unit]
Description=Phuquocdog Mainnet Validator Service
After=network-online.target
Wants=network-online.target

[Service]
User=ubuntu
Group=ubuntu
ExecStart=/home/ubuntu/phuquocdog-node --chain /home/ubuntu/phuquocdog.json --validator --rpc-cors=all --bootnodes /ip4/34.209.135.220/tcp/30333/p2p/12D3KooWEc9LZpacBXG48bVVjZNUaXaQHR4qoW74Xf9tmNw1Sk4P --name  PQD-G01 --base-path /home/ubuntu/data
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

Run a validator as a service

```
sudo systemctl daemon-reload
sudo systemctl start phuquocdog
sudo systemctl status phuquocdog

```

## 💹 Bond PQD

Checkout[ Polkadot Bond ](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-validate-polkadot#bond-dot)documentation.

## 🗝 Set the session keys

Checkout [Polkadot Session Keys](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-validate-polkadot#option-2-cli) documentation.

## 🌠 Validate

Checkout [Polkadot Validate](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-validate-polkadot#validate) documentation.

## 🔱 Links

* [Phu Quoc Dog Testnet Apps](running-a-validator-on-phuquocdog-network.md)
* [Phu Quoc Dog Mainnet Apps](running-a-validator-on-phuquocdog-network.md)
