# Examples of operations on transactions

## Serialize transaction

An example of serialization into a byte array:

```javascript
// Define a transaction
let sendFunds = Exonum.newTransaction({
  author: 'f5602a686807fbf54b47eb4c96b5bac3352a44e7500f6e507b8b4e341302c799',
  service_id: 130,
  message_id: 0,
  fields: [
    { name: 'from', type: Exonum.Hash },
    { name: 'to', type: Exonum.Hash },
    { name: 'amount', type: Exonum.Uint64 }
  ]
})

// Data to be serialized
const data = {
  from: 'f5602a686807fbf54b47eb4c96b5bac3352a44e7500f6e507b8b4e341302c799',
  to: 'f7ea8fd02cb41cc2cd45fd5adc89ca1bf605b2e31f796a3417ddbcd4a3634647',
  amount: 1000
}

// Serialize
let buffer = sendFunds.serialize(data) // [0, 0, 128, 0, 130, 0, 146, 0, 0, 0, 245, 96, 42, 104, 104, 7, 251, 245, 75, 71, 235, 76, 150, 181, 186, 195, 53, 42, 68, 231, 80, 15, 110, 80, 123, 139, 78, 52, 19, 2, 199, 153, 247, 234, 143, 208, 44, 180, 28, 194, 205, 69, 253, 90, 220, 137, 202, 27, 246, 5, 178, 227, 31, 121, 106, 52, 23, 221, 188, 212, 163, 99, 70, 71, 232, 3, 0, 0, 0, 0, 0, 0]
```

Read more about [serialization](../README.md#serialization).

## Sign transaction

An example of transaction signing:

```javascript
// Define a transaction
let sendFunds = Exonum.newTransaction({
  author: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  service_id: 130,
  message_id: 0,
  fields: [
    { name: 'from', type: Exonum.Hash },
    { name: 'to', type: Exonum.Hash },
    { name: 'amount', type: Exonum.Uint64 }
  ]
})

// Data to be signed
const data = {
  from: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  to: 'f7ea8fd02cb41cc2cd45fd5adc89ca1bf605b2e31f796a3417ddbcd4a3634647',
  amount: 1000
}

// Define a signing key pair
const keyPair = {
  publicKey: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  secretKey: '978e3321bd6331d56e5f4c2bdb95bf471e95a77a6839e68d4241e7b0932ebe2b' +
  'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a'
}

// Sign the data
let signature = sendFunds.sign(keyPair.secretKey, data) // '9c7d0e518eb547292b6326faf191dcdb2d97a48a0d0570dec955d3cc3f3bd1e6f6ca4a306675fecc2c144c2b636dfb2254c958b77cd27ea2d17fa1462f67080c'
```

Read more about [data signing](../README.md#sign-data).

## Verify signed transaction

An example of signature verification:

```javascript
// Define a transaction
let sendFunds = Exonum.newTransaction({
  author: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  service_id: 130,
  message_id: 0,
  fields: [
    { name: 'from', type: Exonum.Hash },
    { name: 'to', type: Exonum.Hash },
    { name: 'amount', type: Exonum.Uint64 }
  ]
})

// Data that has been signed
const data = {
  from: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  to: 'f7ea8fd02cb41cc2cd45fd5adc89ca1bf605b2e31f796a3417ddbcd4a3634647',
  amount: 1000
}

// Define a signing key pair
const keyPair = {
  publicKey: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  secretKey: '978e3321bd6331d56e5f4c2bdb95bf471e95a77a6839e68d4241e7b0932ebe2b' +
  'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a'
}

// Signature obtained upon signing using secret key
const signature = 'c304505c8a46ca19454ff5f18335d520823cd0eb984521472ec7638b312a0f5b' +
 '1180a3c39a50cbe3b68ed15023c6761ed1495da648c7fe484876f92a659ee10a'

// Verify the signature
let result = sendFunds.verifySignature(signature, keyPair.publicKey, data) // true
```

Read more about [signature verification](../README.md#verify-signature).

## Get a transaction hash

Note, the transaction **must be signed** before the hash is calculated.

Example of calculation of a transaction hash:

```javascript
// Define a transaction
let sendFunds = Exonum.newTransaction({
  author: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  service_id: 130,
  message_id: 0,
  fields: [
    { name: 'from', type: Exonum.Hash },
    { name: 'to', type: Exonum.Hash },
    { name: 'amount', type: Exonum.Uint64 }
  ]
})

// Data
const data = {
  from: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  to: 'f7ea8fd02cb41cc2cd45fd5adc89ca1bf605b2e31f796a3417ddbcd4a3634647',
  amount: 1000
}

// Define a signing key pair
const keyPair = {
  publicKey: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  secretKey: '978e3321bd6331d56e5f4c2bdb95bf471e95a77a6839e68d4241e7b0932ebe2b' +
  'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a'
}

// Sign the data
const signature = sendFunds.sign(keyPair.secretKey, data)

// Add a signature field
sendFunds.signature = signature

// Get the hash
let hash = sendFunds.hash(data) // 'a0bd9da74d8329abe6ab7131a4a941e0bf6e5e2dded1197c6f75bbca42c81544'
```

Read more about [hashes](../README.md#hash).

## Send transaction

```javascript
// Define a transaction
let sendFunds = Exonum.newTransaction({
  author: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  service_id: 130,
  message_id: 0,
  fields: [
    { name: 'from', type: Exonum.Hash },
    { name: 'to', type: Exonum.Hash },
    { name: 'amount', type: Exonum.Uint64 }
  ]
})

// Define transaction explorer address
const explorerBasePath = 'http://127.0.0.1:8200/api/explorer/v1/transactions'

// Data
const data = {
  from: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  to: 'f7ea8fd02cb41cc2cd45fd5adc89ca1bf605b2e31f796a3417ddbcd4a3634647',
  amount: 1000
}

// Define a signing key pair
const keyPair = {
  publicKey: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  secretKey: '978e3321bd6331d56e5f4c2bdb95bf471e95a77a6839e68d4241e7b0932ebe2b' +
  'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a'
}

// Send transaction
sendFunds.send(explorerBasePath, data, keyPair.secretKey).then(response => {
  // ...
})
```

## Send multiple transactions

```javascript
// Define a transaction
let sendFunds = Exonum.newTransaction({
  author: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  service_id: 130,
  message_id: 0,
  fields: [
    { name: 'from', type: Exonum.Hash },
    { name: 'to', type: Exonum.Hash },
    { name: 'amount', type: Exonum.Uint64 }
  ]
})

// Define transaction explorer address
const explorerBasePath = 'http://127.0.0.1:8200/api/explorer/v1/transactions'

// Data
const transactions = [
  {
    data: {
      from: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
      to: 'f7ea8fd02cb41cc2cd45fd5adc89ca1bf605b2e31f796a3417ddbcd4a3634647',
      amount: 1000
    },
    type: sendFunds
  },
  {
    data: {
      from: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
      to: 'd45fd5adc89ca1bf605b2e31f796a3417ddbcd4a3634647f7ea8fd02cb41cc2c',
      amount: 250
    },
    type: sendFunds
  }
]

// Define a signing key pair
const keyPair = {
  publicKey: 'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a',
  secretKey: '978e3321bd6331d56e5f4c2bdb95bf471e95a77a6839e68d4241e7b0932ebe2b' +
  'fa7f9ee43aff70c879f80fa7fd15955c18b98c72310b09e7818310325050cf7a'
}

// Send transactions queue
Exonum.sendQueue(explorerBasePath, transactions, keyPair.secretKey).then(response => {
  // ...
})
```
