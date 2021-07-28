# Running a RPC node

PhuQuoc Doge Foundation provides the RPC services for the public. Sometimes it's necessary to run a self hosted PhuQuoc Doge RPC service if the public services can't satisfy your needs.

With a self hosted PhuQuoc Doge RPC service you could gain below benefits:

* Faster access speed - a Self-hosted RPC node could provide better performance
* Better security - transactions could be sent to to the self-hosted RPC server instead of the public service.
* Better Availability

PhuQuoc Doge is a fully decentralized network, any people can setup a PhuQuoc Doge node by following this tutorial!

## 🍀 Types Of Phu Quoc Dog RPC Nodes

Generally speaking, there are two kind of RPC nodes:

* **Archive node** An archive node keeps all the past blocks data. And client can't query data in any of the past blocks.
* **Full node** A full is node is pruned. which means it keeps only a few of the past blocks data\(256 by default, which could be adjusted using the `--pruning` command line arguments.

An archive nodes consumes much more disk spaces it stores more data than a full node. You need to take the decision based on your business model and requirements. E.g. block explorer and historical analysis tools normally requires an archive node to query the full historical data. Wallets on the other hand normally only requires a full node to be able to query the current state\(e.g. the balance of an account\) and submit transactions to the PhuQuoc Doge Network.

## 🛠 Hardware requirements

* **CPU** - Recent released high end cpu, e.g. Intel 10700/Amd 5800X.
* **Memory** - 32GB for Testnet, 64GB for Sakura and Mainnet.
* **Storage** - 300GB SSD, Storage usage could increase by time, you might need to increase the capacity as the chain data grows..
* **OS**: Linux, Debian/Ubuntu LTS distributions are recommended.

## Prepare Environment

We'll use [docker](https://docs.docker.com/engine/) and [docker-compose](https://docs.docker.com/compose/) to run the validator in this guide. You need to install docker and docker-compose firstly. Please follow the installation guide in the docs.

* [Docker Install Document](https://docs.docker.com/engine/install/)
* [Docker-Compose Install Document](https://docs.docker.com/compose/install/)

{% hint style="info" %}
We're using docker to simplify the setup process. You can use the tools which you're familiar with.
{% endhint %}

### 🛰 Firewall Setup

Below ports need to be exposed:

* **30333** - The p2p port of the chain
* _**9933** - The http endpoint of the RPC service_
* _**9944** - The websocket endpoint of the RPC service._

{% hint style="info" %}
**You may not expose 9933/9944 ports directly.** Instead a reverse proxy server could be setup in front and proxy requests to the rpc backend.
{% endhint %}

### 📁 Create Directories

Create the config and data directories using below command:

```bash
sudo mkdir -p /opt/data/
sudo mkdir -p /opt/compose/
# secure the data access
sudo chmod 0700 /opt/data
sudo chmod 0700 /opt/compose
```

## ⚙ Setup PhuQuoc Doge Rpc Node

Currently we only have **PhuQuoc Doge Testnet**\(iris\) and **PhuQuoc Doge Mainnet**\(ivy\) launched.

Rpc Configuration for PhuQuoc Doge Mainnet will be updated later.

TODO

{% hint style="info" %}
You can edit the `docker-compose.yaml` and include your customizations by updating below arguments:

* image: the docker image used to launch the node, for PhuQuoc Doge Testnet, use `cloverio/clover-iris:0.1.15.` For a full list of clover networks please check out the [PhuQuoc Doge Network List](https://github.com/phuquocdog/docs/tree/1500cf0c0a387d667a5363e1071b2077d97114ba/quick-start/clover-network-list.md) page.
* --_name_:  The node name of your validator, the name could be found in the telemetry node list
* _--pruning_: we're using the `archive` mode for the pruning argument, which means it will keep all the historical block data. You can provide numeric parameters for it, to let it just keep the provided number of blocks data.
* _--ws-extenral/--rpc-external:_ it enable the outer access for the RPC service.
{% endhint %}

## 🚀 Bring up the RPC node

Use below command to bring up the validator node:

TODO

## 📡 Post Setup

You may want to setup a reverse proxy server or load balancer for the RPC service. There're some known tools for you to start with, please checkout:

* [Nginx](https://www.nginx.com/) - High Performance Load Balancer, Web Server, & Reverse Proxy
* [Caddy](https://caddyserver.com/) -  Powerful, enterprise-ready, open source web server with automatic HTTPS written in Go

