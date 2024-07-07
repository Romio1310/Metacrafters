# DeFi Empire: A Simple DeFi Kingdom Clone

## Overview

DeFi Empire is a project aimed at creating a decentralized finance (DeFi) gaming platform on the Avalanche network. This project provides the foundational framework for a DeFi Kingdom clone, where players can collect, build, and battle with their digital assets, earning rewards through various game activities.

## Features

- Custom EVM subnet on Avalanche
- Native currency for in-game transactions
- Smart contracts for token management and asset vaults
- Integration with MetaMask

## Prerequisites

Before starting, ensure you have the following installed:

- Unix Computer (MacOS or Linux)
- [Node.js](https://nodejs.org/)
- [Avalanche CLI](https://github.com/ava-labs/avalanche-cli)
- [Solidity](https://soliditylang.org/)
- [Remix IDE](https://remix.ethereum.org/)
- [MetaMask](https://metamask.io/)

## Getting Started

### Step 1: Install Avalanche CLI

1. Download and install the Avalanche CLI:
   ```sh
   curl -sL https://raw.githubusercontent.com/ava-labs/avalanche-cli/main/scripts/install.sh |
   ```
2. Adding Avalanche-CLI to Your PATH
```sh 
export PATH=~/bin:$PATH
```
To add it to your path permanently, add an export command to your shell initialization script. If you run bash, use `.bashrc.` If you run zsh, use `.zshrc.`

```sh 
export PATH=~/bin:$PATH >> .bashrc
```

### Step 2: Initialize a New Subnet
1. Create a new subnet:
```sh
avalanche subnet create DeFiEmpireSubnet
```
Follow the prompts to configure your subnet.

### Step 3: Deploy the Subnet
1. Deploy the subnet:
    ```sh
    avalanche subnet deploy DeFiEmpireSubnet
    ```
### Step 4: Add Your Subnet to MetaMask
1. Open MetaMask and click on the network dropdown at the top.

2. Select "Add Network" at the bottom.

3. Fill in the details of your custom subnet:

- Network Name: DeFiEmpireSubnet
- New RPC URL: (Get this URL from your Avalanche subnet deployment output)
- Chain ID: (Get this ID from your Avalanche subnet deployment output)
- Currency Symbol: AVAX
- Block Explorer URL: (Optional, if you have a block explorer for your subnet)
4. Click "Save" to add the network.

#### Obtaining Tokens from Your Subnet
1. During the subnet deployment, you will be shown a private key.

2. Import this private key into MetaMask to access the funds associated with it:

- Open MetaMask and click on the account icon at the top right.
- Select "Import Account."
- Paste the private key provided during subnet deployment.
- Click "Import."
- You should now see the tokens associated with this private key in your MetaMask wallet.
3. You should now see the tokens associated with this private key in your MetaMask wallet.


### Step 5: Deploy the Smart Contracts
1. Open Remix IDE.

2. Connect Remix to MetaMask using the Injected Provider.
3. Create two files in Remix: customToken.sol and assetVault.sol.

`customToken.sol`
```sh
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.17;

    contract CustomToken {
        uint public totalTokens;                                                 // Total supply of tokens
        mapping(address => uint) public tokenBalance;                            // Mapping to track balances
        mapping(address => mapping(address => uint)) public authorizedAllowance; // Allowances for delegated spending
        string public tokenName = "Solidity Example Token";                      // Name of the token
        string public tokenSymbol = "SET";                                       // Symbol of the token
        uint8 public decimalUnits = 18;                                          // Number of decimal units

        event TokensTransferred(address indexed from, address indexed to, uint value);       // Event: Token transfer
        event AllowanceApproved(address indexed owner, address indexed spender, uint value); // Event: Allowance approval


        function transferTokens(address recipient, uint amount) external returns (bool) {    //transfers tokens to a specified address
            tokenBalance[msg.sender] -= amount;
            tokenBalance[recipient] += amount;
            emit TokensTransferred(msg.sender, recipient, amount);
            return true;
        }


        function approveAllowance(address spender, uint amount) external returns (bool) {    //approves the passed address to spend the specified amount of tokens on behalf of msg.sender
            authorizedAllowance[msg.sender][spender] = amount;                               //spender The address to spend the funds
            emit AllowanceApproved(msg.sender, spender, amount);                             //The amount of tokens to be spent
            return true;
        }


        function transferTokensFrom(                                                         //transfers tokens from one address to another
            address sender,                                                                  //the address which you want to send tokens from
            address recipient,                                                               //the address which you want to transfer to
            uint amount                                                                      //the amount of tokens to be transferred
        ) external returns (bool) {
            authorizedAllowance[sender][msg.sender] -= amount;
            tokenBalance[sender] -= amount;
            tokenBalance[recipient] += amount;
            emit TokensTransferred(sender, recipient, amount);
            return true;
        }


        function mintTokens(uint amount) external {                                          //mints new tokens and assigns them to msg.sender
            tokenBalance[msg.sender] += amount;
            totalTokens += amount;
            emit TokensTransferred(address(0), msg.sender, amount);
        }


        function burnTokens(uint amount) external {                                          //burns tokens from msg.sender
            tokenBalance[msg.sender] -= amount;
            totalTokens -= amount;
            emit TokensTransferred(msg.sender, address(0), amount);
        }
    }

    ```
`assetVault.sol`
```sh
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.17;

    interface ICustomERC20 {
        function totalTokens() external view returns (uint);                                       // Get total tokens

        function tokenBalance(address account) external view returns (uint);                       // Get token balance of account

        function transferTokens(address recipient, uint amount) external returns (bool);           // Transfer tokens to recipient

        function authorizedAllowance(address owner, address spender) external view returns (uint); // Get allowance for spender

        function approveAllowance(address spender, uint amount) external returns (bool);           // Approve allowance for spender

        function transferTokensFrom(
            address sender,
            address recipient,
            uint amount
        ) external returns (bool);                                                           // Transfer tokens on behalf of sender

        event TokensTransferred(address indexed from, address indexed to, uint value);       // Event: Token transfer
        event AllowanceApproved(address indexed owner, address indexed spender, uint value); // Event: Allowance approval
    }

    contract AssetVault {
        ICustomERC20 public immutable tokenContract;       // ERC20 token contract instance

        uint public totalShares;                           // Total shares issued
        mapping(address => uint) public shareBalance;      // Share balances


        constructor(address _tokenContract) {                                                        //Constructor to set the token contract
            tokenContract = ICustomERC20(_tokenContract);                                            //_tokenContract Address of the ERC20 token contract
        }


        function mintShares(address to, uint shares) private {                                       //Mints shares to a specified address
            totalShares += shares;                                                                   //to The address to receive shares
            shareBalance[to] += shares;
        }


        function burnShares(address from, uint shares) private {                                     //burns shares from a specified address
            totalShares -= shares;                                                                   //from The address to burn shares from
            shareBalance[from] -= shares;
        }


        function depositAssets(uint amount) external {                                               //deposits tokens into the vault and mints shares
            uint shares;
            if (totalShares == 0) {
                shares = amount;
            } else {
                shares = (amount * totalShares) / tokenContract.tokenBalance(address(this));
            }

            mintShares(msg.sender, shares);
            tokenContract.transferTokensFrom(msg.sender, address(this), amount);
        }


        function withdrawAssets(uint shares) external {                                              //withdraws tokens from the vault by burning shares
            uint amount = (shares * tokenContract.tokenBalance(address(this))) / totalShares;        //shares The number of shares to burn
            burnShares(msg.sender, shares);
            tokenContract.transferTokens(msg.sender, amount);
        }
    }
    ```
4. Compile and deploy the contracts using Remix.

### Step 6: Test Your Application
1. Use Remix to interact with your deployed smart contracts.
2. Deploy tokens, pools, and more using the provided methods in the contracts.

## Points to Remember
1. Always verify contract addresses and network configurations before interacting with the contracts.

2. Keep your private keys secure and never share them publicly.
3. Test thoroughly in a development environment before deploying to the mainnet.
4. Regularly update your dependencies and smart contracts to ensure security and performance.

## Help
If you encounter any issues or need further assistance, consider the following resources:

- Avalanche Documentation
- Remix Documentation
- Solidity Documentation
- MetaMask Support
- Avalanche Discord Community
#### Bonus: 
You can contact me if you need any assistance.🙂
## Conclusion
This project demonstrates the foundational elements of creating a DeFi Kingdom clone on Avalanche. By setting up a custom EVM subnet, deploying a custom token, and creating an asset vault, we have established the core components needed for a decentralized finance gaming platform. Further enhancements can include implementing game activities, integrating with the Avalanche wallet, and adding features like leaderboards and achievements.





