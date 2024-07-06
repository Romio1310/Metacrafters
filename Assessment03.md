# SchoolGradingSystem - Solidity Smart Contract

This Solidity program is a simple smart contract that demonstrates the basic syntax and functionality of error handling in Solidity. The purpose of this program is to serve as a starting point for those who are new to Solidity and want to understand how to implement error handling using `require()`, `revert()`, and `assert()` statements in a real-life scenario of a school grading system.

## Description

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract includes functions that showcase the usage of `require()`, `revert()`, and `assert()` statements for error handling within the context of a school grading system. This program serves as a straightforward introduction to Solidity error handling and can be used as a foundation for more complex projects in the future.

## Getting Started

### Executing the Program

To run this program, you can use Remix, an online Solidity IDE. Follow these steps to get started:

1. Go to the Remix website at [Remix Ethereum](https://remix.ethereum.org/).

2. Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a `.sol` extension (e.g., `SchoolGradingSystem.sol`). Copy and paste the following code into the file:

    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.7;

    contract SchoolGradingSystem {
        address public owner;
        mapping(string => uint8) private grades;

        event GradeAssigned(string student, uint8 grade);
        event GradeUpdated(string student, uint8 grade);

        constructor() {
            owner = msg.sender;
        }

        modifier onlyOwner() {
            require(msg.sender == owner, "Only the owner can perform this action"); // Ensures that only the owner can make changes in the code
            _;
        }

        function assignGrade(string memory _student, uint8 _grade) public onlyOwner { // Implementation of require() statement
            require(_grade >= 0 && _grade <= 100, "Grade must be between 0 and 100");
            grades[_student] = _grade;
            emit GradeAssigned(_student, _grade);
        }

        function updateGrade(string memory _student, uint8 _grade) public onlyOwner { // Implementation of revert() statement
            require(_grade >= 0 && _grade <= 100, "Grade must be between 0 and 100");
            if (grades[_student] == 0) {
                revert("Student has no grade assigned yet");
            }
            grades[_student] = _grade;
            emit GradeUpdated(_student, _grade);
        }

        function getGrade(string memory _student) public view returns (uint8) { // Implementation of assert() statement
            uint8 grade = grades[_student];
            assert(grade != 0); // Assuming a grade of 0 means no grade assigned
            return grade;
        }
    }
    ```

3. To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.7" (or another compatible version), and then click on the "Compile SchoolGradingSystem.sol" button.

4. Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar.

5. Select the "SchoolGradingSystem" contract from the dropdown menu, and then click on the "Deploy" button.

6. Once the contract is deployed, you can interact with it by calling its functions:
   - To test the `assignGrade` function, input a student name and a grade between 0 and 100.
   - To test the `updateGrade` function, input a student name with an existing grade and a new grade between 0 and 100.
   - To test the `getGrade` function, input a student name with an assigned grade.

## Examples

- **Assign Grade:** 
    - Input: `assignGrade("Alice", 85)`
    - Output: Event `GradeAssigned` emitted with student `Alice` and grade `85`.

- **Update Grade:** 
    - Input: `updateGrade("Alice", 90)`
    - Output: Event `GradeUpdated` emitted with student `Alice` and grade `90`.

- **Get Grade:** 
    - Input: `getGrade("Alice")`
    - Output: Returns `90` if the grade was previously updated.

---

Feel free to explore and modify the code to better understand error handling in Solidity. This contract provides a simple yet powerful foundation for learning and developing more complex smart contracts with robust error handling mechanisms.
