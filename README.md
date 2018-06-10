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
