# Block verification

An example of block verification:

```javascript
const data = {
  block: {
    height: '2',
    prev_hash: '5107fe929f173a8fbe609ef907797daab959c6838eb26e074d80534c772e879a',
    proposer_id: 3,
    state_hash: '5f59a6b7810f2cde8a90a4b281c5722d0718cda07f1f321e531c5305ed3baf0e',
    tx_count: 3,
    tx_hash: '09224d3618942784363789a34e016f6f8e683f2ec96a5b9c51c23a02bca2ae1d'
  },
  precommits: [
    {
      payload: {
        block_hash: '7de0d426f0f287849f89e5758015aca00f2e85eda28d2c38581519e0f1de8105',
        height: '2',
        propose_hash: 'e000ec445f25b61d2ac9d38882cffcd59aa02c08a30b2173c5526b89dccd1fcd',
        round: 1,
        time: {
          nanos: 336073000,
          secs: '1537799426'
        },
        validator: 3
      },
      message: 'e6264b7f37f1fc2b4719d89a1360c25ad8b98e9723b485080382761ede1f318201000300020000000000000001000000e000ec445f25b61d2ac9d38882cffcd59aa02c08a30b2173c5526b89dccd1fcd7de0d426f0f287849f89e5758015aca00f2e85eda28d2c38581519e0f1de810502f5a85b00000000281108142da1ea5a2eb4b058a37a69ffb721b7f16c319a4fa1fd34c29efc9bedec454382f9c606a6574349d65be17154465eeb68c4558ca5a1e68a5cc8537aaf81ed780e'
    },
    {
      payload: {
        block_hash: '7de0d426f0f287849f89e5758015aca00f2e85eda28d2c38581519e0f1de8105',
        height: '2',
        propose_hash: 'e000ec445f25b61d2ac9d38882cffcd59aa02c08a30b2173c5526b89dccd1fcd',
        round: 1,
        time: {
          nanos: 336482000,
          secs: '1537799426'
        },
        validator: 0
      },
      message: '2bcd527a39ed80e7da4b767f402b6959cd74ce6980ce0a28c8b2e8a11c99b1f101000000020000000000000001000000e000ec445f25b61d2ac9d38882cffcd59aa02c08a30b2173c5526b89dccd1fcd7de0d426f0f287849f89e5758015aca00f2e85eda28d2c38581519e0f1de810502f5a85b00000000d04e0e14b7235d000fe404a4b9695c0a08c4fc763c9012685b0b37abb0e5b24425e98813c7f1b3a3c8c5cf31e97ada34d63830669ddb072bfc637e16c8d5922538121901'
    },
    {
      payload: {
        block_hash: '7de0d426f0f287849f89e5758015aca00f2e85eda28d2c38581519e0f1de8105',
        height: '2',
        propose_hash: 'e000ec445f25b61d2ac9d38882cffcd59aa02c08a30b2173c5526b89dccd1fcd',
        round: 1,
        time: {
          nanos: 338473000,
          secs: '1537799426'
        },
        validator: 2
      },
      message: 'c9decf2e0d150eec438242c37e628cc2eb5c45d6b18fb8b75c3f9be6529825a401000200020000000000000001000000e000ec445f25b61d2ac9d38882cffcd59aa02c08a30b2173c5526b89dccd1fcd7de0d426f0f287849f89e5758015aca00f2e85eda28d2c38581519e0f1de810502f5a85b0000000028b02c1426a2f9e45be72e3cc986eaa8b3a351d6bc8742653c11ba9fc37e1739addfc535bec2a203ebe345a1bbe637fdb3ce4d63974b20e721928b26a471cc6399d73809'
    }
  ]
}
const validators = [
  '2bcd527a39ed80e7da4b767f402b6959cd74ce6980ce0a28c8b2e8a11c99b1f1',
  '48dbd790d25e0705f2077b1406b4eb64ccf0dd33a8a2215bb840f26f05c6bc1e',
  'c9decf2e0d150eec438242c37e628cc2eb5c45d6b18fb8b75c3f9be6529825a4',
  'e6264b7f37f1fc2b4719d89a1360c25ad8b98e9723b485080382761ede1f3182'
]

Exonum.verifyBlock(data, validators) // true
```
