# Using Docker

#### The easiest way

The easiest/faster option to run Phuquocdog in Docker is to use the latest release images. These are small images that use the latest official release of the Phuquocdog binary, pulled from our package repository.

_**Following examples are running on westend chain and without SSL. They can be used to quick start and learn how Polkadot needs to be configured. Please find out how to secure your node, if you want to operate it on the internet. Do not expose RPC and WS ports, if they are not correctly configured.**_

Let's first check the version we have. The first time you run this command, the Phuquocdog docker image will be downloaded. This takes a bit of time and bandwidth, be patient:

```
// Some code
$ docker run --rm -it phuquocdog/node:latest --version
phuquocdog-node 3.0.0-eba31c8-x86_64-linux-gnu

```

You can also pass any argument/flag that Phuquocdog supports:

```
// Some code
$ docker run --rm -it phuquocdog/node:latest --chain dev --name "PqdDocker"
2021-12-11 13:57:58 Phuquocdog Node    
2021-12-11 13:57:58 ✌️  version 3.0.0-eba31c8-x86_64-linux-gnu    
2021-12-11 13:57:58 ❤️  by Phu Quoc Dog <https://phuquoc.dog>, 2017-2021    
2021-12-11 13:57:58 📋 Chain specification: Development    
2021-12-11 13:57:58 🏷 Node name: PqdDocker    
2021-12-11 13:57:58 👤 Role: FULL    
2021-12-11 13:57:58 💾 Database: RocksDb at /phuquocdog-node/.local/share/phuquocdog-node/chains/dev/db/full    
2021-12-11 13:57:58 ⛓  Native runtime: node-270 (phuquocdog-official-0.tx2.au10)    
2021-12-11 13:57:58 🔨 Initializing Genesis block/state (state: 0x288f…1ef2, header-hash: 0x8b4c…0643)    
2021-12-11 13:57:58 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
2021-12-11 13:58:00 ⏱  Loaded block-time = 12s from block 0x8b4caa99533f5ba9204732b0e1123380ebebc34d2a349f566293aa07e13a0643    
```

Once you are done experimenting and picking the best node name :) you can start Phuquocdog  as daemon, exposes the Phuquocdog ports and mount a volume that will keep your blockchain data locally.

To start a Phuquocdog node on default rpc port 9933 and default p2p port 30333 use the following command. If you want to connect to rpc port 9933, then must add Phuquocdog startup parameter: `--rpc-external`.

```
// Some code
docker run --name pqddev -d -p 30333:30333 -p 9933:9933 -v ~/pqddata:/data phuquocdog/node:latest --chain dev --rpc-external --rpc-cors all
// see log
docker logs -f pqddev
2021-12-11 14:01:11 Phuquocdog Node    
2021-12-11 14:01:11 ✌️  version 3.0.0-eba31c8-x86_64-linux-gnu    
2021-12-11 14:01:11 ❤️  by Phu Quoc Dog <https://phuquoc.dog>, 2017-2021    
2021-12-11 14:01:11 📋 Chain specification: Development    
2021-12-11 14:01:11 🏷 Node name: different-level-0206    
2021-12-11 14:01:11 👤 Role: FULL    
2021-12-11 14:01:11 💾 Database: RocksDb at /phuquocdog-node/.local/share/phuquocdog-node/chains/dev/db/full    
2021-12-11 14:01:11 ⛓  Native runtime: node-270 (phuquocdog-official-0.tx2.au10)    
2021-12-11 14:01:12 🔨 Initializing Genesis block/state (state: 0x288f…1ef2, header-hash: 0x8b4c…0643)    
2021-12-11 14:01:12 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
2021-12-11 14:01:14 ⏱  Loaded block-time = 12s from block 0x8b4caa99533f5ba9204732b0e1123380ebebc34d2a349f566293aa07e13a0643    
2021-12-11 14:01:14 👶 Creating empty BABE epoch changes on what appears to be first startup.    
2021-12-11 14:01:14 Using default protocol ID "sup" because none is configured in the chain specs    
2021-12-11 14:01:14 🏷 Local node identity is: 12D3KooWB4iMZBcg1pp2E9vubk8CBTu8mgWkdhTb6dXL5NVQkJVn    
2021-12-11 14:01:14 📦 Highest known block at #0    
2021-12-11 14:01:14 〽️ Prometheus exporter started at 127.0.0.1:9615    
2021-12-11 14:01:14 Listening for new connections on 127.0.0.1:9944.    

```

#### Running to mainnet Phu Quoc Dog

Above we just running for enviroment develop, to running a validator on mainnet you just rechange the command above like this:

```
// Some code
mkdir ~/pqddata
chmod 777 -R ~/pqddata
docker run --name pqd-mainnet -d -p 30333:30333 -p 9933:9933 -v ~/pqddata:/data phuquocdog/node:latest --chain /node/phuquocdog.json --rpc-external --rpc-cors all
```

Then check log and data you should see something like this

```
// See data
ls ~/pqddata/chains/
phuquocdog_main_network

// See log

docker logs -f pqd-mainnet
2021-12-11 14:14:11 Phuquocdog Node    
2021-12-11 14:14:11 ✌️  version 3.0.0-eba31c8-x86_64-linux-gnu    
2021-12-11 14:14:11 ❤️  by Phu Quoc Dog <https://phuquoc.dog>, 2017-2021    
2021-12-11 14:14:11 📋 Chain specification: Phuquocdog Main Network    
2021-12-11 14:14:11 🏷 Node name: elderly-caption-0260    
2021-12-11 14:14:11 👤 Role: FULL    
2021-12-11 14:14:11 💾 Database: RocksDb at /phuquocdog-node/.local/share/phuquocdog-node/chains/phuquocdog_main_network/db/full    
2021-12-11 14:14:11 ⛓  Native runtime: node-270 (phuquocdog-official-0.tx2.au10)    
2021-12-11 14:14:12 🔨 Initializing Genesis block/state (state: 0x4bba…5ae2, header-hash: 0xbbe6…1d84)    
2021-12-11 14:14:12 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
2021-12-11 14:14:14 ⏱  Loaded block-time = 12s from block 0xbbe65b0d6c309386a01b852ce910965607a926ac8263c640559d783539851d84    
2021-12-11 14:14:14 👶 Creating empty BABE epoch changes on what appears to be first startup.    
2021-12-11 14:14:14 🏷 Local node identity is: 12D3KooWMPzHDVLBBwkQuKFsZfyE6Fhwsvq3wqNZq2qD6RsRxhvA    
2021-12-11 14:14:14 📦 Highest known block at #0    
2021-12-11 14:14:14 〽️ Prometheus exporter started at 127.0.0.1:9615    
2021-12-11 14:14:14 Listening for new connections on 127.0.0.1:9944.    
2021-12-11 14:14:17 🔍 Discovered new external address for our node: /ip4/52.12.232.246/tcp/30333/ws/p2p/12D3KooWMPzHDVLBBwkQuKFsZfyE6Fhwsvq3wqNZq2qD6RsRxhvA    
2021-12-11 14:14:19 ⚙️  Syncing, target=#47930 (5 peers), best: #128 (0x167b…14f4), finalized #0 (0xbbe6…1d84), ⬇ 23.7kiB/s ⬆ 3.1kiB/s    
2021-12-11 14:14:21 [#196] 🗳  creating a snapshot with metadata SolutionOrSnapshotSize { voters: 3, targets: 3 }    
2021-12-11 14:14:21 [#196] 🗳  Starting signed phase round 1.    
2021-12-11 14:14:21 [#200] 🗳  Starting unsigned phase round 1 enabled true. 
```

Congrant. Now you have a part with Phu Quoc Dog Network!
