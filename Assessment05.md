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

## Installation

To deploy and interact with the contract:

1. Clone this repository:

   ```bash
   git clone https://github.com/Romio1310/Metacrafters.git
2. Navigate to the project directory:   
    ```bash
    cd mytoken
3. Install Dependencies:
    ```bash
    # No dependies required for the contract itself

## Usage
### Deploying wih the Contract
Deploy the contract using a Solidity development environment like Remix or Hardhat.        

### Interacting with the Contract
1. **Mint Token:** 
- Connect to the contract owner's address.
- Call the mint function with the recipient's address and amount to mint.

2. **Burn Tokens:**
- Connect to any token holder's address.
- Call the burn function with the amount of tokens to burn.

## Example
``` bash
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
