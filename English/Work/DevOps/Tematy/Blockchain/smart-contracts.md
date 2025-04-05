# Smart Contracts Basics

## What are Smart Contracts?
- **Definition**: Self-executing programs stored on a blockchain that automatically enforce agreements
- **Key Traits**:
  - Immutable: Once deployed, unchangeable
  - Deterministic: Same input = same output
  - Transparent: Code and execution are public

## How They Work
1. **Code**: Written in a language like Solidity (Ethereum)
2. **Deploy**: Compiled and uploaded to blockchain
3. **Trigger**: Activated by transactions or conditions
4. **Execute**: Runs automatically, updates blockchain state
5. **Verify**: Nodes confirm execution

## Example (Solidity)
```solidity
pragma solidity ^0.8.0;
contract SimpleStorage {
    uint public storedData;
    function set(uint x) public {
        storedData = x;
    }
}
```
- Deploys a contract to store a number
- `set()` updates the value

## Key Features
- **Conditions**: If/then logic (e.g., "If payment received, release funds")
- **Gas**: Fee for computation (paid in crypto, e.g., ETH)
- **State**: Persistent data stored on-chain
- **Events**: Log info for external apps to read

## Platforms
- **Ethereum**: Most popular, uses Solidity
- **Solana**: High-speed, uses Rust
- **Binance Smart Chain**: EVM-compatible, lower fees
- **Tezos**: Formal verification for security

## Use Cases
- **DeFi**: Lending, trading (e.g., Uniswap)
- **NFTs**: Ownership and transfer logic
- **Voting**: Transparent, tamper-proof systems
- **Escrow**: Automated fund release

## Development Tools
- **Remix**: Online IDE for Solidity
- **Truffle**: Framework for testing/deployment
- **Hardhat**: Advanced dev environment
- **OpenZeppelin**: Secure contract templates

## Workflow
1. **Write**: Code in Solidity
   ```solidity
   contract Escrow {
       address payer;
       address payee;
       uint amount;
       function release() public {
           require(msg.sender == payer);
           payable(payee).transfer(amount);
       }
   }
   ```
2. **Test**: Use local blockchain (e.g., Ganache)
3. **Deploy**: To testnet (e.g., Sepolia) or mainnet
4. **Interact**: Via Web3.js/Ethers.js
   ```javascript
   const contract = new ethers.Contract(address, abi, signer);
   await contract.release();
   ```

## Challenges
- **Bugs**: Immutable code means errors are permanent
  - e.g., The DAO hack (2016)
- **Gas Costs**: Expensive for complex logic
- **Security**: Vulnerable to reentrancy, overflow attacks

## Best Practices
- **Audit**: Get code reviewed
- **Test**: Cover edge cases
- **Upgradeability**: Use proxy patterns
- **Keep Simple**: Minimize gas and attack surface

> **Tip**: Start with Remix and a testnet to build your first contract!