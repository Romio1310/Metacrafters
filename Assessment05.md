# MyToken - ERC20 Token Contract

## Overview

This repository contains the source code for `MyToken`, an ERC20 token smart contract developed using Solidity. The contract includes basic functionalities such as token minting by the owner and token burning by any token holder.

## Features

- **Token Name:** DoughCoin (DOG)
- **Token Symbol:** DOG
- **Standard:** ERC20
- **Owner Functions:**
  - `mint(address to, uint256 amount)`: Allows the owner to mint tokens to a specified address.
- **User Functions:**
  - `burn(uint256 amount)`: Allows any token holder to burn their tokens.

## Prerequisites

To deploy and interact with this contract, you will need:

- [Node.js](https://nodejs.org/)
- [npm](https://www.npmjs.com/)
- [Remix IDE](https://remix.ethereum.org/)

## Installation

### Cloning the Repository

1. Clone this repository:
    ```bash
    git clone https://github.com/Romio1310/Metacrafters.git
    ```
2. Navigate to the project directory:
    ```bash
    cd mytoken
    ```
3. Install Dependencies:
    ```bash
    # No dependencies required for the contract itself
    ```

## Usage

### Deploying with Remix IDE

1. Open [Remix IDE](https://remix.ethereum.org/).
2. Create a new file and copy the contract code into it.
3. Compile the contract using the Solidity compiler.
4. Deploy the contract using an Ethereum wallet like MetaMask.

### Interacting with the Contract

1. **Mint Tokens:**
    - Connect to the contract owner's address.
    - Call the `mint` function with the recipient's address and the amount to mint.

2. **Burn Tokens:**
    - Connect to any token holder's address.
    - Call the `burn` function with the amount of tokens to burn.

## Contract Details

### Example Contract Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    constructor() ERC20("DoughCoin", "DOG") Ownable(msg.sender) {}

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }
}
```
## Types of Functions
### Owner Functions
    
- `mint(address to, uint256 amount)`: Allows the contract owner to mint tokens to a specified address.
### User Functions
- `burn(uint256 amount)`: Allows any token holder to burn their tokens.


## Conclusion
By following these instructions, you can deploy and interact with the MyToken ERC20 smart contract, leveraging Remix IDE for development and testing. The project demonstrates the essential functionalities of token minting, burning, and transferring in a decentralized environment.

## Note

This `README.md` file now includes all the sections and information you requested, properly formatted and structured.
