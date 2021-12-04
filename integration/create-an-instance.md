# Create an instance

We have the API installed, we have an understanding of what will actually be exposed and how the API knows what to expose. So down the rabbit hole we go - let's create an actual API instance, and then take it from there -

```
// Some code
// Import
import { ApiPromise, WsProvider } from '@polkadot/api';

...
// Construct
const wsProvider = new WsProvider('wss://rpc01.phuquoc.dog');
const api = await ApiPromise.create({ provider: wsProvider });

// Do something
console.log(api.genesisHash.toHex());
```

Where other code is included (or just some previous boilerplate is used), you will see `...` in most of the examples. This is not due to laziness, but rather just to keep things straight and to the point.

### Providers[​](https://polkadot.js.org/docs/api/start/create#providers) <a href="#providers" id="providers"></a>

Focusing on the construction, any API requires a provider and we create one via the `const wsProvider = new WsProvider(...)`. By default, if none is provided to the API it will construct a default `WsProvider` instance to connect to `ws://127.0.0.1:9944`.

We generally recommend always specifying the endpoint since in most cases we want to connect to an external node and even for local nodes, it is always better being explicit, less magic that can make you wonder in the future.

At this time the only provider type that is fully supported by the API is the WebSocket version. Polkadot/Substrate really comes alive with possibilities once you have access to bi-directional RPCs such as what WebSockets provide. (It is technically possible to have some limited capability via bare-HTTP, but at this point WebSockets is the only fully-operational and supported version - always remember that it is just "upgraded HTTP".)

### API Instance[​](https://polkadot.js.org/docs/api/start/create#api-instance) <a href="#api-instance" id="api-instance"></a>

The API creation is done via the `ApiPromise.create` interface which is a shortcut version for calling `new` and then waiting until the API is connected. Without the `async` syntax, this would be,

```
// Some code
ApiPromise
  .create({ provider: wsProvider }).isReady
  .then((api) =>
    console.log(api.genesisHash.toHex())
  );
```

In most cases we would suggest using the `.create` shortcut, which really just takes care of the following boilerplate that otherwise needs to be provided -

```
// Some code
/ Create the instance
const api = new ApiPromise({ provider: wsProvider });

// Wait until we are ready and connected
await api.isReady;

// Do something
console.log(api.genesisHash.toHex());
```
