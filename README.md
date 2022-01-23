# web3-journey-notes
notes and caveats to remember for my web3 journey (solidity, web3js/ether.js, etc.)

## Solidity

- Global variables:
  1. `msg`: msg.sender <-address of the person who called the contract
  2.    

- `state` vars stored on eth blockchain permanently  
- types:
  1. `bools`
  2. `string` 
  3. `uint`- `uint8`,`uint16`,`uint32`,`uint64`,`uint256` <- default
  4. `int`- can be neg & positive
  5. `address` - can be `payable` or `nonpayable`
  6. `array` - can be `fixed` or `dynamic`
    - fixed: uint[2] fixed <- fixedArray of uint with length 2
    - dynamic: uint[] dynamicArray
    - Person[] person <- dynamic array of structs
  7. `enum`
  8. `mappings` - essentially a key-value store for storing and looking up data
  ```
  mapping (key => value) public storeSomething;
  ```
  10. `struct` - similar to creating an object/class
  ```
  struct Person {
    uint age;
    string name;
    }
    ```
- `**` is the operation for squaring

- `public` vs `private`:
    - `public` = accesible everywhere
    - `private` = only accessible by the contract it's declared in

- `internal` vs `external`:
    - `internal` = `private` + it's also accessible to contracts that inherit from this contract
    - `external` = that these functions can ONLY be called outside the contract — they can't be called by other functions inside that contract
 
- `view` vs `pure` :
    - `view` means, only viewing the data but not modifying it
    - `pure` means, not even accessing any data in the app

- `keecak256`:
```
A hash function basically maps an input into a random 256-bit hexadecimal number. A slight change in the input will 
cause a large change in the hash. It expects a single parameter of type bytes. This means that we have to "pack" 
any parameters before calling it using abi.encodePacked
 ```
 - `events`: Events are a way for the contract to communicate that something happened on the blockchain to the app front-end
 
 create event
 ```
 event IntegersAdded(uint x, uint y, uint result);
 ```
 emit event
 ```
 function add(uint _x, uint _y) public returns (uint) {
  uint result = _x + _y;
  // fire an event to let the app know the function was called:
  emit IntegersAdded(_x, _y, result);
  return result;
}
```
- `require` keyword, makes it so that the function will throw an error and stop executing if some condition is not true
- `storage` vs `memory`  
  - `storage` = variables stored permanently on the blockchain  
  - `memory` = temporary, and are erased between external function calls to the contract
  should try to use `memory` as much as possible to keep gas low

**Interface**

create an interface by declaring it (can return multiple vars)
```
contract NumberInterface {
  function getNum(address _myAddress) public view returns (uint);
}
```
instantiate interface, and from there `interface` will have access to `getNum`
```
NumberInterface interface = NumberInterface(_contractAddress)
```

- handling multiple return values:
 ```
   (a, b, c) = multipleReturns(); <-assigns all returned values
   (,,c) = multipleReturns(); <- select specific values
  ```

*conventions*
- underscore function parameter names `(address _address)`
- private function names begin with an underscore `function _privateFunc`
