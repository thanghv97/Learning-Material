## Kiểm tra một địa chỉ  có phải là địa chỉ hợp đồng thông minh hay không

### Implement
  + code solidity  
  ```
  function isContract(address _addr) private returns (bool isContract){
    uint32 size;
    assembly {
      size := extcodesize(_addr)
    }
    return (size > 0);
  }
  ```
  + openzeppelin
  ```
  import "@openzeppelin/contracts/utils/Address.sol";

  if (Address.isContract(_to)) {
    ...
  }
  ```

### Note

### reference
  + https://ethereum.stackexchange.com/questions/15641/how-does-a-contract-find-out-if-another-address-is-a-contract
