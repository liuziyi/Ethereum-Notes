# Ethereum

- Links
  - [Ethereum and Solidity: The Complete Developer's Guide (Section 1), Udemy](https://www.udemy.com/ethereum-and-solidity-the-complete-developers-guide/learn/v4/content)

## 1. Ethereum Network
  - Ethereum networks are used to transfer money and store data
  - There are many different ethereum networks: test networks, private networks and one main ethereum network
  - Networks are formed by one of more nodes
  - Each node is a machine running an ethereum client
  - Anyone can run a node
  - Each node can contain a full copy of the blockchain
  - The 'blockchain' is a database that stores a record of every transaction that has ever taken place

  ![](images/1-EN/ethereum-network.png)

## 2. Interacting/connecting with the Ethereum Networks

  ![](images/2-EN-connection/connecting.png)

  - Traditional Architecture vs Ethereum Architecture
    - The server in the ethereum architecture can still send a HTML document and some JS assets down to the browser. However, it's role is dramatically diminished.
    - Whenever a user tries to change some data, it does not reach back out to the server. The server is not at all involved in that process. Instead the ethereum application running inside the browser will make use of web3 which communicates with metamask, metamask creates a transaction signs it with the user's private key and sends that transaction to the ethereum network. (** The only way for a user to change data is through the use of their public and private keys.)
    - With the ethereum architecture all the responsibility for writing data to some database from the server will be shifted over to the client, which means that the client needs to be a lot more intelligent and have a lot more functionality built into it as compared to a traditional architecture.

  ![](images/2-EN-connection/traditional-architecture.png)

  ![](images/2-EN-connection/ethereum-architecture.png)

## 3. Ethereum Accounts
  - Metamask
    - Each account has three distinct pieces of info: account address, public key and private key. These three pieces of info is what constitutes an account.
    - The account address can be thought of as something that's similar to an email address or a username. It's a unique identifier that can be shared with anyone in the world and it tells other people who you are that identifies your account in some fashion.
    - The public and private key combined together forms a password of sorts. They are used to authorize the sending of funds from your account to other accounts. If someone does not have the private key to an account, they don't have access to any of the funds that are assigned to that account.
    - The account address, public key and private key are all stored as hexadecimal numbers

    ![](images/3-EA/metamask-account.png)

    - Unlike emails where there are two distinct accounts for gmail and hotmail, one account is used across all the different networks.

    ![](images/3-EA/metamask-networks.png)

## 4. Ether
  - Get ether from rinkeby-faucet.com or rinkeby.faucet.io

  ![](images/4-ether/ether.png)

## 5. Transactions
  - Transactions are sent to just one node in the network.

  ![](images/5-transactions/transaction-network.png)

  ![](images/5-transactions/transaction-node.png)

  ![](images/5-transactions/transaction-node-block.png)

  - Transfer of money between two parties
    - Transaction object: External to External Account Transactions

    ![](images/5-transactions/transfer-$.png)

  - Creating a contract
    - Deployment

    ![](images/5-transactions/deployment.png)

    - Transaction object: External Account to Create Contract Transactions
      - Main difference between a money sending transaction and a contract creation transaction is, the to field is left blank for contract creation transactions

    ![](images/5-transactions/contract-creation.png)

## 6. Block Time

## 7. Smart Contracts
  - A smart contract is an account controlled by code

  ![](images/7-smartContracts/contract-account.png)

  - External Accounts vs Contract Accounts
    - External accounts: live in their own universe that's completely decoupled from any individual network. One account can be used to connect to the Main network, Ropsten, Kovan or Rinkeyby.
    - Contract accounts: only specific to one individual network. When a contract account is created using the smart contract, it is created on one specific network and cannot be accessed across networks

  ![](images/7-smartContracts/EAvsCA.png)

  - Deployment
    - When the contract code is deployed, an instance of the contract is created.
    - One contract code can be deployed multiple times to one network or multiple networks.

  ![](images/7-smartContracts/deployment.png)

    - The relationship between the contract source and contract instance is very similar to the relationship between a class and an instance in the programming world.

## 8. Solidity

  ![](images/8-solidity/solidity.png)

  - Basic solidity types

  ![](images/8-solidity/solidity-basicTypes.png)

  - Integer ranges

  ![](images/8-solidity/solidity-integerRanges.png)

  - Reference types

  ![](images/8-solidity/solidity-refTypes.png)

    - Arrays (e.g. uint[] public myArray): the function that gets generated for an array in solidity does not return the entire array (to retrieve an entire array need to create a function (below)). It accepts one argument and that's the index of the element that we want to retrieve from the array.

    ```solidity
    uint[] public numbersArray; 

    function Numbers() public {
      numbersArray.push(10);
      numbersArray.push(100);
      numbersArray.push(1000);
    }

    function getArrayLength() public view returns (uint) {
      return numbersArray.length;
    }

    function getFirstElement() public view returns (uint) {
      return numbersArray[0];
    }

    // To retrieve an entire array
    function getNumbers() public view returns (uint[]) {
      return numbersArray;
    }
    ```
    - Struct
      - A custom type that you can define similar to address, uint, string, etc. You can define the struct with a name and associated properties inside of it.
      - It's very similar to a class and if we want to make use of it we have to first create an instance of it.
      - Models some given individual object e.g a struct that represents a user, which will store their age, first and last name.
      - Can reference each user by their ethereum address, which can be done by creating a mapping

      ```solidity
      struct User {
        uint age;
        string fName;
        string lName;
      }
      ```
      - Instance creation syntax
        - Every field of the struct has to be initialized everytime an instance of a struct is created. 
        - When we initialize properties of a struct, we only have to initialize the value types. There's no need to add any code to initialize a reference type e.g a mapping.

      ![](images/8-solidity/struct-instance.png)

      ```solidity
      function createUser(uint age, string fName, string, lName) public {
        User newUser = User({
          age: age,
          fName: fName,
          lName: lName
        });
      }
      ```

    - Mapping
      - A hash table, which consists of key types and value type pairs.
      - It can be defined like any other variable type.
      - The mapping below is referred to as users, which has a key of type address and the value type is a Struct that was created above.

      ```solidity
      mapping(address => User) users;
      ```
    - Arrays vs Mappings
      - Arrays: the search inside of an array is linear which means for every additional record that is added to the array, it's going to take a slightly larger amount of time to execute a search. So if there are 10 records inside of an array it might take 10 seconds to search through and if there are 100 records it might take 100 seconds.
      - Mappings: no matter how many pieces of data is stored inside a mapping, it's always going to take the exact same amount of time to execute a search. For e.g. it'll only take one second to look up a given user whether there is one user or 10000 users inside the mapping.

      ![](images/8-solidity/ArrayvsMapping.png)

    - JS Objects vs Mappings
      - Common JS operations
        1. Can easily retrieve all the keys that a JS object has.
        2. Can easily retrieve all the different values that the object has.
        3. Can retrieve a single key using the bracket notation.
        4. Will get back a value of undefined when accessing a key that does not exist.

      ```javascript
      const spanishColors = {
        red: 'rojo',
        green: 'verde',
        orange: 'naranja'
      }

      Object.keys(spanishColors) -> ["red", "green", "orange"]
      Object.values(spanishColors) -> ["rojo", "verde", "naranja"]
      spanishColors["red"] -> rojo
      spanishColors["yellow"] === undefined -> True
      ```
      - Mappings
        1. Cannot get a list of keys. We don't know what keys a mapping has.
        2. Cannot get a list of all the different values that a mapping has.
        3. Cannot loop through a mapping and print out all the different values it has. So it's not possible to write a for loop that iterates through all the values.
        4. All we can do is do a lookup of values e.g. spanishColors["red"].
        5. Mappings are only good for single value lookups, they're not good for storing information that we want to iterate over sometime in the future.
        6. All values exist. For e.g. if we put in some value that does not exist (yellow) to the hashing function, we'll get back some index and the index will be looked up inside the mapping. And rather than telling us that there is no value at that particular index, it'll return some default value for that element. The default value that we get back from mappings depends on the value type of the values inside of the mapping e.g. a empty string if the values were strings. This makes it hard to know whether or not a value exists.

        ![](images/8-solidity/mappings-keys.png)

        ![](images/8-solidity/mappings-values.png)

  - Message ('msg') global variable
    - Available both when a transaction is sent and with a call

    ![](images/8-solidity/msg-transaction.png)

    ![](images/8-solidity/msg-call.png)

    - Properties

    ![](images/8-solidity/msg-properties.png)

  - Function modifiers
    - Helps to reduce the amount of code to write.
    - It includes use cases such as restricting who has the ability to run a given function.
    - When the modifier is added to any of the other functions in the contract, the solidity compiler will take all of the code out of that function and add it to the modifier in place of that underscore.

  ```solidity
  function withdraw() public restricted {
    ...
    ...
  }

  modifier restricted() {
    require(msg.sender == owner);
    _;
  }
  ```
  - Storage vs Memory

  ![](images/8-solidity/StoragevsMemory1.png)

  ![](images/8-solidity/StoragevsMemory2.png)

  - The byte code is the actual byte code that will be deployed to the ethereum network.
  - The ABI is what enables apps to interact with the deployed smart contracts.

  ![](images/8-solidity/solidity-compiler.png)

  - The JS code has no ability to interact with the byte code that has been deployed to the ethereum network so need the ABI to do the translation.

  ![](images/8-solidity/ABI.png)

## 9. Remix
  - remix.ethereum.org
  - Remix editor
    - Remix is not just a code editor, it also hosts a tiny fake ethereum network that can be used to simulate deploying and interacting with the contract.

  ![](images/9-remix/remix1.png)

  - Select JavaScript VM to deploy the contract to the in-browser virtual ethereum network. This will boot up the internal virtual network which automatically creates a handful of different accounts each of which are assigned 100 ether. Making it really easy for testing.

  ![](images/9-remix/remix2.png)

## 10. Contract
  - Contract structure
  - Function declarations
    - Declarations

    ![](images/10-contract/fnDeclarations.png)

    - Types

    ![](images/10-contract/fnTypes.png)

    - Running contract functions  
      - To change anything on the blockchain, need to submit a transaction

      ![](images/10-contract/changes.png)

      ![](images/10-contract/CallvsSet.png)

## 11. Wei vs Ether

  ![](images/11-EtherWei/EthervsWei.png)

## 12. Gas

## 13. Mnemonic Phrases
  - https://iancoleman.io/bip39/

  ![](images/13-mnemonicPhrases/MP1.png)

  ![](images/13-mnemonicPhrases/MP2.png)

  ![](images/13-mnemonicPhrases/MP3.png)
