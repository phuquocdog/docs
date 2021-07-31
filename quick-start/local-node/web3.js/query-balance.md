---
description: Use Web3.js to Query Balance on PhuQuoc Doge
---

# Query Balance

## Query Balance

We can easily do this by leveraging the Ethereum compatibility features of Phu Quoc Dog.

First let's create a file _balance.js_ under the project we've created. Here we just query the balance of the genesis account, and the genesis account is endowed with **10,000,000** ETH by your local Phu Quoc Dog node under the development mode. To get the balances of the account, we need to make an asynchronous function that uses the `web3.eth.getBalance(address)` command. We can take advantage of the `web3.utils.fromWei()` function to transform the balance into a more readable number in ETH.

The file looks like this:

```typescript
const Web3 = require('web3')

const web3 = new Web3(new Web3.providers.HttpProvider('http://localhost:9933'));
const GENESIS_ACCOUNT = '0x16206a7f064c7d77C6d8e3eD8601c9AA435419cE';

async function getBalance(account) {
  const balance = await web3.eth.getBalance(account);
  const balanceOfEther = web3.utils.fromWei(balance, "ether");
  console.log(`${account} has balance: ${balanceOfEther} ETH`);
}

getBalance(GENESIS_ACCOUNT);
```

### Running the Script

You can run the above script using the command :

```text
node balance.js
```

The output of the execution is as follows:

## 

```typescript
0x16206a7f064c7d77C6d8e3eD8601c9AA435419cE: 10,000,000 ETH
```

