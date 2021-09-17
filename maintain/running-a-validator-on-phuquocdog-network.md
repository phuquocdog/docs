# Running a validator on Phu Quoc Dog Network

This guide will instruct you on how to set up a Phu Quoc Doge validator node on Phu Quoc Dog networks \(Testnet/Mainnet\).

## 👉 Must Read Before Start.

Running a validator is a serious thing, you have a lot of responsibility for the staked tokens of you and nominators. You take the risk of losing your staked tokens as a slash might happen if your validator node is not properly configured. Please make sure you or your team have the necessary knowledge to run a validator node.

[Polkadot Wiki ](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-validate-polkadot)has an awesome introduction of running a validator node on the [Polkadot network](https://polkadot.network/). As a member of the Polkadot ecosystem, Phu Quoc Dog follows a similar process to run and setup a validator node. We may skip some basics steps in this tutorial.

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

```text
rustup update
```

If not, this command will fetch the latest version of Rust and install it.

```text
curl https://sh.rustup.rs -sSf | sh -s -- -y
```

Add the required toolchains with rustup

```text
source $HOME/.cargo/env
rustup toolchain add nightly-2021-05-11
rustup target add wasm32-unknown-unknown --toolchain nightly-2021-05-11
rustup target add x86_64-unknown-linux-gnu --toolchain nightly-2021-05-11

```

Verify your installation.

```text
rustc --version
```

Note - if you are using OSX and you have Homebrew installed, you can issue the following equivalent command INSTEAD of the previous one:

```text
brew install cmake pkg-config openssl git llvm
```

#### 

#### Install & Configure Network Time Protocol \(NTP\) Client

[NTP](https://en.wikipedia.org/wiki/Network_Time_Protocol) is a networking protocol designed to synchronize the clocks of computers over a network. NTP allows you to synchronize the clocks of all the systems within the network. Currently it is required that validators' local clocks stay reasonably in sync, so you should be running NTP or a similar service. You can check whether you have the NTP client by running:

If you are using Ubuntu 18.04 / 20.04, NTP Client should be installed by default.

```text
timedatectl
```

If NTP is installed and running, you should see `System clock synchronized: yes` or a similar message. If you do not see it, you can install it by executing:

```text
sudo apt-get install ntp
```

ntpd will be started automatically after install. You can query ntpd for status information to verify that everything is working:

```text
sudo ntpq -p
```

## ⚙ Setup PhuQuoc Doge Validator Node

Currently, we only have **PhuQuoc Doge Testnet**\(**Quarks**\) and **Phu Quoc Dog Mainnet**\(Bosons\) launched. Phu Quoc Dog Testnet opens for validators to join. _Phu Quoc Doge Mainnet operates in the POA mode and maintained by 6 nodes belongs to the Phu Quoc Dog foundation_.

Validator Configuration for Phu Quoc Dog Mainnet will be updated later once it's ready for staking and validators can join.

**Build from source**

To build the `Polkadex` binary from the [Node](https://github.com/phuquoc/node) repository on GitHub using the source code available in the v0.4.1-rc5 release.

```text
git clone https://github.com/phuquoc/node.git
cd node
```

Build native code with the cargo release profile.

```text
cargo build --release
```

This step will take a while \(generally 10 - 40 minutes, depending on your hardware\).

#### 

#### Synchronize Chain Data

Download `customSpecRaw.json` file for the Polkadex Public Testnet

```text
cd $HOME
curl -O -L https://raw.githubusercontent.com/phuquocdog/node/master/node/res/phuquocdog.json
```

You can begin syncing your node by running the following commands if you do not want to start in validator mode right away:

```text
/home/ubuntu/phuquocdog --chain /home/ubuntu/phuquocdog.json --validator --rpc-cors=all --bootnodes /ip4/34.209.135.220/tcp/30333/p2p/12D3KooWDzJJ1DHAqbzT5RZbXji6powSkj5ZioSHSLnYXiqRD34q --name  Mynode03 --base-path /home/ubuntu/data
```

## 🚀 Bring up the validator node

Use the below command to bring up the validator node:

## 💹 Bond PQD

Checkout[ Polkadot Bond ](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-validate-polkadot#bond-dot)documentation.

## 🗝 Set the session keys

Checkout [Polkadot Session Keys](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-validate-polkadot#option-2-cli) documentation.

## 🌠 Validate

Checkout [Polkadot Validate](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-validate-polkadot#validate) documentation.

## 🔱 Links

* [Phu Quoc Dog Testnet Apps](running-a-validator-on-phuquocdog-network.md)
* [Phu Quoc Dog Mainnet Apps](running-a-validator-on-phuquocdog-network.md)

