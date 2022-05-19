# Issues in POA running
## Geth
  + [Account Cannot Transfer](#account-cannot-transfer)
  + [Synchronize failed](#synchronize-failed)

### Synchronize failed
  + Guarantee nodes are connected 

    Using [net.peerCount](#) or [admin.peers](../../Tool/Geth/JSON-RPC%20APIS/admin#admin-peers)
    However, using `net.peerCount` needs to guarantee the flag `--nodiscover` is used. Because the value of `net.peerCount` keeps changing due to the peer discovery mechanism.

  + Check syncing process of a node 
    ```
      > eth.syncing
      false
    ```
    `false` means that your Geth is up to date and is not currently syncing. It keeps importing the latest block to remain up to date. 
  + Check number of block of nodes
    ```
      > eth.blockNumber
      226 
    ```
  + Case
    + Two nodes run 
      > clear data/geth folder of node sync failed, run again to sync again 

### Account Cannot Transfer
  + Check the account is unlocked
    ```
      > personal.listWallets
      [{
          accounts: [{
              address: "0x2d18e713fa424ceafb16da4bebd0395c48e9cdc1",
              url: "keystore:///home/ib-cntt/Project/iFinChain/GethPoA_3/node1/data/keystore/UTC--2022-05-10T07-01-40.277532760Z--2d18e713fa424ceafb16da4bebd0395c48e9cdc1"
          }],
          status: "Unlocked",
          url: "keystore:///home/ib-cntt/Project/iFinChain/GethPoA_3/node1/data/keystore/UTC--2022-05-10T07-01-40.277532760Z--2d18e713fa424ceafb16da4bebd0395c48e9cdc1"
      }, {
          accounts: [{
              address: "0xc6b7635b75df007c4cb322fc3d9d9c6f1dcdd04b",
              url: "keystore:///home/ib-cntt/Project/iFinChain/GethPoA_3/node1/data/keystore/UTC--2022-05-10T07-01-56.835428187Z--c6b7635b75df007c4cb322fc3d9d9c6f1dcdd04b"
          }],
          status: "locked",
          url: "keystore:///home/ib-cntt/Project/iFinChain/GethPoA_3/node1/data/keystore/UTC--2022-05-10T07-01-56.835428187Z--c6b7635b75df007c4cb322fc3d9d9c6f1dcdd04b"
      }]
    ```
    + unlock account 
      + when run node 
        ```
          add flag: --unlock 0x1D635Ba6FBa91AB8a921F44114A8D891433a13FD --password password.txt
        ```
      + after run node 
        ```
          personal.unlockAccount('address', 'password', duration:optional)
        ``` 
