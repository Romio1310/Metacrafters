# Assessment Smart Contract

This Solidity smart contract, named `Assessment`, serves as a basic financial system that allows depositing and withdrawing funds, while enforcing ownership and handling errors gracefully.

## Description

The `Assessment` contract is designed to manage Ether deposits and withdrawals. It ensures only the owner can deposit or withdraw funds and includes error handling to manage insufficient balance scenarios. The contract emits events for both deposit and withdrawal actions to provide transparency.

## Getting Started

### Prerequisites

To deploy and interact with this contract, you will need:

- [Node.js](https://nodejs.org/)
- [npm](https://www.npmjs.com/)
- [Hardhat](https://hardhat.org/)
- An Ethereum wallet (e.g., MetaMask)
- [Solidity](https://soliditylang.org/)

### Installing

1. Clone the repository in your desired location:
    ```sh
    git clone https://github.com/MetacrafterChris/SCM-Starter.git
    ```
2. Open the cloned folder.
3. Install dependencies:
    ```sh
    npm install
    ```

## Running the Project

After cloning the GitHub repository, you will want to do the following to get the code running on your computer:

1. Inside the project directory, in the terminal type:
    ```sh
    npm i
    ```
2. Open two additional terminals in your VS Code.
3. In the second terminal, type:
    ```sh
    npx hardhat node
    ```
4. In the third terminal, deploy the contract to the local network:
    ```sh
    npx hardhat run --network localhost scripts/deploy.js
    ```
5. Back in the first terminal, launch the front-end:
    ```sh
    npm run dev
    ```
    This will start the application at [http://localhost:3000/](http://localhost:3000/).

## Contract Details

### State Variables

- **address payable public owner:** Stores the address of the contract owner.
- **uint256 public balance:** Tracks the current balance of the contract.

### Functions

- **function getBalance() public view returns (uint256):** Returns the current balance of the contract.
- **function deposit(uint256 _amount) public payable:** Allows the owner to deposit funds into the contract. Emits a Deposit event.
- **function withdraw(uint256 _withdrawAmount) public:** Allows the owner to withdraw funds from the contract. Emits a Withdraw event.

### Events

- **event Deposit(uint256 amount):** Emitted when funds are deposited.
- **event Withdraw(uint256 amount):** Emitted when funds are withdrawn.

### Error Handling

- **error InsufficientBalance(uint256 balance, uint256 withdrawAmount):** Custom error for handling insufficient balance during withdrawal.

## Smart Contract Code

### assessment.sol
```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;

//import "hardhat/console.sol";

contract Assessment {
    address payable public owner;
    uint256 public balance;

    event Deposit(uint256 amount);                                                  // two events: Deposit and Withdraw
    event Withdraw(uint256 amount);

    constructor(uint initBalance) payable {                                         //initializing and sets the contract deployer
        owner = payable(msg.sender);
        balance = initBalance;
    }

    function getBalance() public view returns(uint256){                             // use to view the current balance of the account.
        return balance;
    }

    function deposit(uint256 _amount) public payable {
        uint _previousBalance = balance;

        require(msg.sender == owner, "You are not the owner of this account");      //this will ensure for the owner

        balance += _amount;                                                         

        assert(balance == _previousBalance + _amount);                              // assert transaction completed successfully

        // emit the event
        emit Deposit(_amount);
    }

    // custom error
    error InsufficientBalance(uint256 balance, uint256 withdrawAmount);

    function withdraw(uint256 _withdrawAmount) public {
        require(msg.sender == owner, "You are not the owner of this account");
        uint _previousBalance = balance;
        if (balance < _withdrawAmount) {
            revert InsufficientBalance({
                balance: balance,
                withdrawAmount: _withdrawAmount
            });
        }

        balance -= _withdrawAmount;                                 //withdraws the given amount

        assert(balance == (_previousBalance - _withdrawAmount));    //assert the balance is correct

        emit Withdraw(_withdrawAmount);                             // emit the event
    }
}


```
## Hardhat Configuration
### hardhat.config.js
```sh
require("@nomicfoundation/hardhat-toolbox");

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.17",
};
```
By following these instructions, you can deploy and interact with the Assessment smart contract, leveraging Hardhat's development environment and tools for testing and deployment.

## Help

This `README.md` file now provides a comprehensive and structured guide for setting up, running, and understanding the `Assessment` smart contract.
