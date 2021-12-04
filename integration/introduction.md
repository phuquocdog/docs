# Introduction

The API provides application developers the ability to query a node and interact with the Polkadot or Substrate chains using Javascript. Here you will find documentation and examples to get you started.

[Jump right in](https://polkadot.js.org/docs/api/start) and get an overview on using the API in your projects, from installation all the way through to making it do magic. Have things working and want tips? The [cookbook](https://polkadot.js.org/docs/api/cookbook) provides some tips and tricks.

For oft-repeated questions, the [FAQ](https://polkadot.js.org/docs/api/FAQ) may have what you are looking for.

**All documents you can see at** [**https://polkadot.js.org/docs/api/start**](https://polkadot.js.org/docs/api/start)\*\*\*\*

## Simple Connect

The following example shows how to instantiate a Polkadot API object and use it to connect to a node using ApiPromise.

```
// Some code
// Required imports
const { ApiPromise, WsProvider } = require('@polkadot/api');

async function main () {
  // Initialise the provider to connect to the local node
  const provider = new WsProvider('wss://rpc01.phuquoc.dog');

  // Create the API and wait until ready
  const api = await ApiPromise.create({ provider });

  // Retrieve the chain & node information information via rpc calls
  const [chain, nodeName, nodeVersion] = await Promise.all([
    api.rpc.system.chain(),
    api.rpc.system.name(),
    api.rpc.system.version()
  ]);

  console.log(`You are connected to chain ${chain} using ${nodeName} v${nodeVersion}`);
}

main().catch(console.error).finally(() => process.exit());
```

### Generate address

The Keyring allows you to manage a set of keys in a consistent environment, allows you to perform operations on these keys (such as sign/verify) and never exposes the secretKey to the outside world.

To get started, follow the [getting started](https://polkadot.js.org/docs/keyring/start) journey for installation and use. For oft-repeated questions, the [FAQ](https://polkadot.js.org/docs/keyring/FAQ) may have what you are looking for.

Checkout on [https://polkadot.js.org/docs/keyring](https://polkadot.js.org/docs/keyring)
