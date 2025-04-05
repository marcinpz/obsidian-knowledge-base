# [[web3]] Basics

## What is Web3?
- **Definition**: A decentralized internet leveraging blockchain technology
- **Evolution**: 
  - Web1: Static pages (read-only)
  - Web2: Interactive, centralized (read-write)
  - [[web3]]: Decentralized, user-owned (read-write-execute)
- **Core Idea**: Shift control from centralized entities (e.g., Big Tech) to users via cryptography and peer-to-peer networks

## Key Components
- **[[blockchain]]**: Distributed ledger for trustless transactions
  - e.g., Ethereum, Solana, Polygon
- **[[Smart Contracts]]**: Self-executing code on blockchain
  - Written in Solidity (Ethereum), Rust (Solana), etc.
- **Cryptocurrencies**: Native tokens (e.g., ETH, BTC)
  - Fuel transactions and incentivize network participation
- **Wallets**: Manage keys and interact with Web3
  - e.g., MetaMask, Coinbase Wallet
- **DApps**: Decentralized applications
  - Frontend + smart contract backend

## Networking in Web3
- **Nodes**: Computers running blockchain software
  - Full nodes: Store entire blockchain
  - Light nodes: Query data only
- **P2P**: Peer-to-peer communication, no central server
- **RPC**: Remote Procedure Call endpoints
  - e.g., Connect to Ethereum via `https://mainnet.infura.io`
- **IPFS**: InterPlanetary File System
  - Decentralized file storage (content-addressed)

## Tools for DevOps/Programmers
- **Web3.js / Ethers.js**: JavaScript libraries for Ethereum interaction
- **Truffle/Hardhat**: Smart contract development frameworks
- **Ganache**: Local blockchain for testing
- **Metamask**: Browser extension for wallet/DApp integration
- **Infura/Alchemy**: Hosted node providers

## Basic Workflow
1. **Setup Wallet**: Create a wallet (e.g., MetaMask)
2. **Get Test ETH**: Use faucets (e.g., Rinkeby, Sepolia)
3. **Write Contract**: Code in Solidity
   ```solidity
   pragma solidity ^0.8.0;
   contract Hello {
       string public message = "Hello, Web3!";
   }
   ```
4. **Deploy**: Use Truffle or Remix to deploy to a network
5. **Interact**: Call contract functions via Web3.js
   ```javascript
   const contract = new web3.eth.Contract(abi, address);
   contract.methods.message().call().then(console.log);
   ```

## Key Terms
- **Gas**: Fee for computation on Ethereum
- **Nonce**: Transaction counter for an account
- **DeFi**: Decentralized Finance (e.g., lending, trading)
- **NFTs**: Non-Fungible Tokens (unique digital assets)

## Challenges
- **Scalability**: High gas fees, slow transactions
- **Security**: Smart contract bugs (e.g., reentrancy attacks)
- **UX**: Complex for non-technical users

> **Note**: Start with testnets (e.g., Sepolia) to experiment without real funds!