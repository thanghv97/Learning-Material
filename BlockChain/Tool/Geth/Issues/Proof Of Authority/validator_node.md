# VALIDATOR NODE
A validator node is a node that includes a sealer. Therefore, a new node cannot mine if that node does not include a sealer.
  + [check sealer](#check-sealer)
  + [add/remove validator node](#add-remove-validator-node)

## Check sealer
when a run node doesn't include sealer but enable `--mine` or [miner.start()](#), that node cannot mine and appear a warning
```
    WARN [05-19|09:42:41.129] Block sealing failed                     err="unauthorized signer"
```

check sealers for initial [block 0] in file `genesis.json` or [clique.getSigners](../../Json-Rpc%20APIs/clique.md#clique-getSigner)
  + genesis.json [block 0]
    ```
    "extraData":"0x000....{addr0}{addr1}...0000"
                0x64ch        sealers      131ch
    ```

  + clique.getSigners
    ```
        > clique.getSigners() // get all sealer at current block
        ["0x0e0ede9c2c2a15211b17afda438219a860b1c8d7", "0x2d18e713fa424ceafb16da4bebd0395c48e9cdc1",            
        0xc69b6868775618cb2f2dab2d8feeaaab2baf3c7b"]

        > clique.getSigners(0) // get all sealer at block 0
        ["0x0e0ede9c2c2a15211b17afda438219a860b1c8d7"]
    ```

## Add Remove validator node
To authorize a new sealer, existing ones can propose it via [clique.propose](../../Json-Rpc%20APIs/clique.md#clique-propose). When more than half the signers proposed it, the authorization comes into effect immediately and the new account can start signing blocks.
  ```
    > clique.propose("0x....", true)
    null
  ```

Similarly, existing signers can propose deauthorizing existing ones via [clique.propose](../../Json-Rpc%20APIs/clique.md#clique-propose). Again if more than half signers deauthorize a signer, it is immediately removed from the list and blocks minted by it are rejected from that point onward.
  ```
    > clique.propose("0x....", false)
    null
  ```