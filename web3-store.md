# Web3 store

This documentation describes the HTTP API for [**Web3.Storage**](https://web3.storage), which allows you to quickly and easily build applications using decentralized data storage persisted by [Filecoin](https://filecoin.io) and available over [IPFS](https://ipfs.io).

### Store files

To store a file on decentralized data storage, you need send a POST request. Method parameters are supplied in positional order.

| Number | Type     | Description                                                                              |
| ------ | -------- | ---------------------------------------------------------------------------------------- |
| 1      | `file[]` | An iterable collection of [Files](https://developer.mozilla.org/en-US/docs/Web/API/File) |

| to be packed into a CAR and uploaded. |             |                                                                                                                                                     |
| ------------------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2                                     | `{options}` | _Optional._ An object whose properties define certain Web3.Storage options and metadata about the files being uploaded. See below for more details. |

An `{options}` object has the following properties that can be used as parameters when calling `put()`:



```
curl "https://api.phuquoc.dog/web3/storage" \
    -X POST \
    -F 'file=@/path/to/pictures/picture.jpg'
    -H "Authorization: Bearer 74305f35862b76db" \
    -H "Content-Type: multipart/form-data" 
```

Result:

```
// Some code
{
    "status": true,
    "message": "File is uploaded",
    "data": {
        "name": "13edf243597e9e92f809ab030147cdde.png",
        "mimetype": "image/png",
        "size": 610388,
        "cid": "bafybeidzrwd5wj64hku4sr6egkhr4wksy67s52wx7qzrgowdt7fcgsyaau",
        "dwebLink": "https://bafybeidzrwd5wj64hku4sr6egkhr4wksy67s52wx7qzrgowdt7fcgsyaau.ipfs.dweb.link/13edf243597e9e92f809ab030147cdde.png"
    }
}
```

### Retrieve files

Retrieve files using the `get()` method. You will need the CID you obtained at upload time that references the CAR for your uploaded files.

Retrieve an [IPFS DAG](https://docs.ipfs.io/concepts/merkle-dag/) (Directed Acyclic Graph) packaged in a CAR file by using `/`web3/storage`{cid}`, supplying the CID of the data you are interested in.



```
// Some code
curl  -X GET https://api.phuquoc.dog/web3/storage/bafybeidzrwd5wj64hku4sr6egkhr4wksy67s52wx7qzrgowdt7fcgsyaau
-H "Content-Type: application/json" \
-H "Authorization : Bearer eyJ0eXAiOi"
```

