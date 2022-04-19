# Cài đặt
## Tạo folder chung GethPoA
  ```
    ~$ mkdir GethPoA
    ~$ cd GethPoa
  ```

## Tạo node 
  ```
    ~/GethPoA$ mkdir node1
    ~/GethPoA$ cd node1
    ~/GethPoA/node1$ geth --datadir "./data" account new
  ``` 
  ```
    INFO [04-13|16:46:56.396] Maximum peer count                       ETH=50 LES=0 total=50
    INFO [04-13|16:46:56.396] Smartcard socket not found, disabling    err="stat /run/pcscd/pcscd.comm: no such file or directory"
    Your new account is locked with a password. Please give a password. Do not forget this password.
    Password: 
    Repeat password: 

    Your new key was generated

    Public address of the key:   0x1D635Ba6FBa91AB8a921F44114A8D891433a13FD
    Path of the secret key file: data/keystore/UTC--2022-04-13T09-47-02.015205959Z--1d635ba6fba91ab8a921f44114a8d891433a13fd

    - You can share your public address with anyone. Others need it to interact with you.
    - You must NEVER share the secret key with anyone! The key controls access to your funds!
    - You must BACKUP your key file! Without the key, it's impossible to access account funds!
    - You must REMEMBER your password! Without the password, it's impossible to decrypt the key!
  ```
  Ta sẽ có 1 account trong node1 với địa chỉ `0x1D635Ba6FBa91AB8a921F44114A8D891433a13FD` và password `123456a@`

## Tạo private chain
  ```
    ~/GethPoA$ puppeth
  ```
  + cấu hình private chain 
    ```
      Please specify a network name to administer (no spaces, hyphens or capital letters please)
      > blockpoa 
    ```
    ```
      What would you like to do? (default = stats)
        1. Show network stats
        2. Configure new genesis
        3. Track new remote server
        4. Deploy network components
      > 2
    ```
    ```
      What would you like to do? (default = create)
        1. Create new genesis from scratch
        2. Import already existing genesis
      > 1
    ```
    set cơ chế đồng thuận cho private chain
    ```
      Which consensus engine to use? (default = clique)
        1. Ethash - proof-of-work
        2. Clique - proof-of-authority
      > 2
    ```
    set accounts cho phép đào block
    ```
      Which accounts are allowed to seal? (mandatory at least one)
      > 0x1D635Ba6FBa91AB8a921F44114A8D891433a13FD
      > 0x
    ```
    set accounts được cấp free ether  
    ```
      Which accounts should be pre-funded? (advisable at least one)
      > 0x1D635Ba6FBa91AB8a921F44114A8D891433a13FD
      > 0x
    ```
    cấp account 0x1 .. 0xff 1 wei
    ```
      Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? (advisable yes)
      > yes
    ```
    set chain/network ID của private chain
    ```
      Specify your chain/network ID if you want an explicit one (default = random)
      > 14333
    ```
  + export cấu hình private chain
    ```
      What would you like to do? (default = stats)    
        1. Show network stats    
        2. Manage existing genesis    
        3. Track new remote server    
        4. Deploy network components    
        > 2
    ```
    ```
      1. Modify existing configurations
      2. Export genesis configurations
      3. Remove genesis configuration
      > 2
    ```
    Save config vào thử mục blockpoa
    ```
      Which folder to save the genesis specs into? (default = current)
        Will create blockpoa.json, blockpoa-aleth.json, blockpoa-harmony.json, blockpoa-parity.json
      > blockpoa
    ```

## Thiết lập node sử dụng cấu hình private chain
  ```
    ~/GethPoA$ cd node1
    ~/GethPoA/Node1$ geth --datadir data/ init ../blockpoa/blockpoa.json 
  ```
## Cấu trúc thư mục


# Run
  + node mine
  
    `after 1.10.8-stable`
    ```
        geth --networkid 14333 --datadir "./data" --bootnodes enode://.... --port 30303 --ipcdisable --syncmode full --http --allow-insecure-unlock --http.corsdomain "*" --http.port 8545 --unlock 0x34785cf6bD1CC94d5ea7D2dcF2Be541A628B53BE --password password.txt --mine console 
    ```

  + node 
    
    `after 1.10.8-stable`
    ```
        geth --networkid 14333 --datadir "./data" --bootnodes enode://.... --port 30303 --ipcdisable --syncmode full --http --allow-insecure-unlock --http.corsdomain "*" --http.port 8545 --unlock 0xf98EC1905AA6D629196eE81De49D8d1B0d3357A8 --password password.txt console 
    ```

### Q&A
  + Nhiều node đào 

  + Time tạo block 
