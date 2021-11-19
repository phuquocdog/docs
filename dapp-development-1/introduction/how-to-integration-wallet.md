# How to integration wallet

#### How to transfer out?

This sample shows how to create a transaction to make a transfer from one account to another.

```
// Some code
// Import the API, Keyring and some utility functions
const { ApiPromise } = require('@polkadot/api');
const { Keyring } = require('@polkadot/keyring');

const BOB = '5FHneW46xGXgs5mUiveU4sbTyGBzmstUspZC92UhjJM694ty';

async function main () {
  // Instantiate the API
  const api = await ApiPromise.create();

  // Constuct the keyring after the API (crypto has an async init)
  const keyring = new Keyring({ type: 'sr25519' });

  // Add Alice to our keyring with a hard-deived path (empty phrase, so uses dev)
  const alice = keyring.addFromUri('//Alice');

  // Create a extrinsic, transferring 12345 units to Bob
  const transfer = api.tx.balances.transfer(BOB, 12345);

  // Sign and send the transaction using our account
  const hash = await transfer.signAndSend(alice);

  console.log('Transfer sent with hash', hash.toHex());
}

main().catch(console.error).finally(() => process.exit());
```

See more example at [https://github.com/phuquocdog/wallet/blob/master/class/wallets/phuquocdog-wallet.js#L217](https://github.com/phuquocdog/wallet/blob/master/class/wallets/phuquocdog-wallet.js#L217)

#### **How to get account/Address balance to check there is enough coins to withdraw?**

Let's dive right in, connect to a general chain and retrieve some information on the current state. Of interest may be retrieving the nonce of a particular account as well as the current balance, this can be achieved via&#x20;

```
// Some code
// Import the API, Keyring and some utility functions
const { ApiPromise,WsProvider } = require('@polkadot/api');
const { Keyring } = require('@polkadot/keyring');

const ADDR = '5CNChyk2fnVgVSZDLAVVFb4QBTMGm6WfuQvseBG6hj8xWzKP';


async function getBalance () {

	const provider = new WsProvider('wss://rpc.phuquoc.dog');
	const api = await ApiPromise.create({provider});
	// Retrieve the last timestamp
	const now = await api.query.timestamp.now();
	const { nonce, data: balance } = await api.query.system.account(ADDR);

	console.log(`${now}: balance of ${balance.free} and a nonce of ${nonce}`);
	console.log('balance for human: ' + balance.free.toHuman());
	console.log(balance);

}
getBalance().catch(console.error).finally(() => process.exit());


```

#### How to transfer out?

Transaction endpoints are exposed, as determined by the metadata, on the `api.tx` endpoint. These allow you to submit transactions for inclusion in blocks, be it transfers, setting information or anything else your chain supports.



```
// Import the API, Keyring and some utility functions
const { ApiPromise,WsProvider } = require('@polkadot/api');
const { Keyring } = require('@polkadot/keyring');
const BN = require('bn.js');

async function transferBalance () {

	// Some mnemonic phrase
	const PHRASE = 'barrel outer about develop dignity nice slab lottery sort album knock salt';

	const provider = new WsProvider('wss://rpc.phuquoc.dog');
	const api = await ApiPromise.create({provider});
	

	// Constuct the keyring after the API (crypto has an async init)
    const keyring = new Keyring({ type: 'sr25519' });

    // Add //Alice to our keyring with a hard-deived path (empty phrase, so uses dev)
    const alice = keyring.addFromUri(PHRASE);

    const decims = new BN(api.registry.chainDecimals);
    const factor = new BN(1).pow(decims);
    const amount = new BN(1).mul(factor);

    // Create a extrinsic, transferring 12345 units to Bob
    const transfer = api.tx.balances.transfer(ADDR, amount);

    // Sign and send the transaction using our account
    const hash = await transfer.signAndSend(alice);

    console.log('Transfer sent with hash', hash.toHex());

}

transferBalance().catch(console.error).finally(() => console.log('------Finish Demo getBalance ----'));
```

