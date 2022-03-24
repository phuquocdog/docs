# Account service

### Create an wallet

To created an wallet on blockchain phuquocdog

HTTP Request: `POST` [`https://account-service.phuquoc.dog`](https://account-service.phuquoc.dog)``

```
//
curl -H "Content-Type: application/json" -X POST https://account-service.phuquoc.dog

```

Sample response:

```
{
    "status": true,
    "mnemonic": {
        "phrase": "trouble strike stairs inherit table luggage wolf nest upon like slam repeat"
    },
    "address": "5EUVQGKHHEus6b2YwkTxD4jtkFeNLcb4kp5DwPV1FLcBngJy"
}
```

### Get address wallet

HTTP Request: `POST` [`https://account-service.phuquoc.dog/phrase`](https://account-service.phuquoc.dog/phrase)``

```
// Some code
data.json
{
  "phrase": "trouble strike stairs inherit table luggage wolf nest upon like slam repeat"
}
curl -d data.json -H "Content-Type: application/json" -X POST https://account-service.phuquoc.dog/pharase

```

Sample response:

```
{
    "status": true,
    "address": "5EUVQGKHHEus6b2YwkTxD4jtkFeNLcb4kp5DwPV1FLcBngJy"
}
```

### Transactions

To send PQD coin use that endpoint below:

HTTP Request: POST https://account-service.phuquoc.dog/transaction

```
// Some code
data.json 
{
    "phrase": "barrel outer about develop dignity nice slab lottery sort album knock salt",
    "amount": 2,
    "address": "5EUVQGKHHEus6b2YwkTxD4jtkFeNLcb4kp5DwPV1FLcBngJy"

}

curl -d data.json -H "Content-Type: application/json" -X POST https://account-service.phuquoc.dog/transaction

```

Sample response:

```
{
    "status": true,
    "hash": "0x01fb33c4417cf3f25ecc43ca3bb4e57b121100099248e8bbbd8570b07a36459e"
}
```
