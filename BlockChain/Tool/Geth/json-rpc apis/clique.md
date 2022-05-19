## clique
  + set
    + [clique.propose](#clique.propose)
  + get
    + [clique.getSigner](#clique.getSigner)
    + [clique.getSigners](#clique.getSigners)
    + [clique.proposals](#clique.proposals)
    + [clique.status](#clique.status)

### clique.propose
  Adds a new authorization proposal that the signer will attempt to push through.
  + If the auth parameter is `true` => the local signer votes for the given address to be included in the set of authorized signers. 
  + If the auth parameter is `false` => the vote is against the address.

  ||||
  |-|-|-|
  |Client|Method invocation|
  |Console|clique.propose(address, auth)|
  ||||

  ```
    > clique.propose("0x0e0ede9c2c2a15211b17afda438219a860b1c8d7", true)
    null
  ```

### clique.getSigner
  Retrieves signer was authorized for the specified block.

  ||||
  |-|-|-|
  |Client|Method invocation|
  |Console|clique.getSigner(blockNumber)|
  ||||

  ```
    > clique.getSigner('0x1') ### block number represented by hex format
    "0x0e0ede9c2c2a15211b17afda438219a860b1c8d7"
  ```

### clique.getSigners
  Retrieves the list of authorized signers at the specified block.
  
  ||||
  |-|-|-|
  |Client|Method invocation|
  |Console|clique.getSigners(blockNumber)|
  ||||

  ```
    > clique.getSigners() ### if dont set blockNumber
    ["0x0e0ede9c2c2a15211b17afda438219a860b1c8d7", "0x2d18e713fa424ceafb16da4bebd0395c48e9cdc1",            
    0xc69b6868775618cb2f2dab2d8feeaaab2baf3c7b"]
  ```

### clique.proposals

### clique.status
