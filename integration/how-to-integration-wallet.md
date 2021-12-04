# How to integration wallet

**How to get account/Address balance to check there is enough coins to withdraw?**

Let's dive right in, connect to a general chain and retrieve some information on the current state. Of interest may be retrieving the nonce of a particular account as well as the current balance, this can be achieved via

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

const ADDR = '5FUZZjdRkb7Z8YC7iTfPyNjtoc5zXvRw4kXqtpeVEituaRom';


async function transferBalance (amount) {

	// Some mnemonic phrase
	const PHRASE = 'barrel outer about develop dignity nice slab lottery sort album knock salt';

	const provider = new WsProvider('wss://rpc.phuquoc.dog');
	const api = await ApiPromise.create({provider});
	

	// Constuct the keyring after the API (crypto has an async init)
    const keyring = new Keyring({ type: 'sr25519' });

    // Add //Alice to our keyring with a hard-deived path (empty phrase, so uses dev)
    const alice = keyring.addFromUri(PHRASE);

    const decims = new BN(api.registry.chainDecimals);
    const factor = new BN(10).pow(decims);
    const amountUnit = new BN(amount).mul(factor);

    //console.log(amountUnit)

    // Create a extrinsic, transferring 12345 units to Bob
    const transfer = api.tx.balances.transfer(ADDR, amountUnit);

    // Sign and send the transaction using our account
    const hash = await transfer.signAndSend(alice);

    console.log('Transfer sent with hash', hash.toHex());

}

transferBalance(10).catch(console.error).finally(() => console.log('------Finish Demo getBalance ----'));


```

In the example above we just send 10PQD to address 5FUZZjdRkb7Z8YC7iTfPyNjtoc5zXvRw4kXqtpeVEituaRom, to send multiple at the same time you need to change

```
// Some code
const hash = await transfer.signAndSend(alice);
```

Tobe

```
// Some code
const hash = await transfer.signAndSend(alice,{ nonce: -1 });
```

If not, you will be get the error like this `Hash:: 1014: Priority is too low: (3752826182276 vs 3752826182276): The transaction has too low priority to replace another transaction already in the pool.`See more [https://polkadot.js.org/docs/api/cookbook/tx/#how-do-i-take-the-pending-tx-pool-into-account-in-my-nonce](https://polkadot.js.org/docs/api/cookbook/tx/#how-do-i-take-the-pending-tx-pool-into-account-in-my-nonce)

#### How to iterator the trancsation list by transaction-ids

You can send a GET request with trancsation id

```
// Some code
GET
https://hasura.phuquoc.dog/api/rest/transactions?id=trancsationid 
```

To get information transaction id `0xc66213c30e88c88e099f297ccd90ead6367b43723fcdb2f863541b6d6f5f8c52`

```
// Some code
https://hasura.phuquoc.dog/api/rest/transactions?id=0xc66213c30e88c88e099f297ccd90ead6367b43723fcdb2f863541b6d6f5f8c52
{
    "extrinsic": [
        {
            "args": "[{\"id\":\"5DM8un9Cn9CjWD9oEAbKcZvU8xGf3HFJC8DJUTQ2jGsgn4hR\"},500000000000000]",
            "block_number": 1852,
            "doc": "[ Same as the [`transfer`] call, but with a check that the transfer will not kill the,  origin account., ,  99% of the time you want [`transfer`] instead., ,  [`transfer`]: struct.Pallet.html#method.transfer,  # <weight>,  - Cheaper than transfer because account cannot be killed.,  - Base Weight: 51.4 µs,  - DB Weight: 1 Read and 1 Write to dest (sender is in overlay already),  #</weight>]",
            "extrinsic_index": 1,
            "fee_details": "{\"inclusionFee\":{\"baseFee\":10000000,\"lenFee\":148000000,\"adjustedWeightFee\":13202109}}",
            "fee_info": "{\"weight\":167334000,\"class\":\"Normal\",\"partialFee\":171202109}",
            "hash": "0xc66213c30e88c88e099f297ccd90ead6367b43723fcdb2f863541b6d6f5f8c52",
            "is_signed": true,
            "method": "transferKeepAlive",
            "section": "balances",
            "signer": "5DAFV7VmRcoxkXQq1xjdFeJrA8tSDyqCZxUfbuqv6DY4BinA",
            "success": true,
            "timestamp": 1637296116
        }
    ]
}
```

Get all history transaction an account

```
// Some code
https://hasura.phuquoc.dog/api/rest/account_transactions?id=xxx
```

For example get transaction send and recived account `5HGnAjebsXJrscjrk7TzCSc4p21faUaMEdTY9Xrp4CLwYKtQ`

```
// Some code
https://hasura.phuquoc.dog/api/rest/account_transactions?id=5HGnAjebsXJrscjrk7TzCSc4p21faUaMEdTY9Xrp4CLwYKtQ
```
