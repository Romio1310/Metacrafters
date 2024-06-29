# ErrorHandling Smart Contract

This Solidity program is a simple smart contract that demonstrates the basic syntax and functionality of error handling in Solidity. The purpose of this program is to serve as a starting point for those who are new to Solidity and want to understand how to implement error handling using `require()`, `revert()`, and `assert()` statements.

## Description

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract includes functions that showcase the usage of `require()`, `revert()`, and `assert()` statements for error handling. This program serves as a straightforward introduction to Solidity error handling, and can be used as a foundation for more complex projects in the future.

## Getting Started

### Executing the Program

To run this program, you can use Remix, an online Solidity IDE. Follow these steps to get started:

1. Go to the Remix website at [Remix Ethereum](https://remix.ethereum.org/).

2. Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a `.sol` extension (e.g., `ErrorHandling.sol`). Copy and paste the following code into the file:

    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.7;

    contract ErrorHandling {
        uint public num = 0; // Initial declaration

        // Function that uses require to validate input
        function testRequire(uint _i) public pure {
            require(_i > 10, "Input must be greater than 10");
        }

        // Function that uses revert to validate input
        function testRevert(uint _i) public pure {
            if (_i <= 10) {
                revert("Input must be greater than 10"); // This will revert with the following error
            }
        }

        // Function that uses assert to check state
        function testAssert() public view {
            assert(num == 0); // Assert will check that num is 0 only.
        }
    }
    ```

3. To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.7" (or another compatible version), and then click on the "Compile ErrorHandling.sol" button.

4. Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar.

5. Select the "ErrorHandling" contract from the dropdown menu, and then click on the "Deploy" button.

6. Once the contract is deployed, you can interact with it by calling its functions:
   - To test the `testRequire` function, input a value greater than 10.
   - To test the `testRevert` function, input a value less than or equal to 10.
   - To test the `testAssert` function, ensure `num` is zero (you can call this function directly to check the condition).

By following these steps, you can execute and test the error handling functions in the contract.

---

Feel free to explore and modify the code to better understand error handling in Solidity. This contract provides a simple yet powerful foundation for learning and developing more complex smart contracts with robust error handling mechanisms.
