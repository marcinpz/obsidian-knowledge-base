# Blockchain Basics

## What is Blockchain?
- **Definition**: A decentralized, distributed ledger recording transactions across a network
- **Core Features**:
  - Immutable: Once written, data can't be altered
  - Transparent: Publicly verifiable
  - Trustless: No central authority needed

## How It Works
1. **Transaction**: User initiates an action (e.g., send 1 ETH)
2. **Block**: Transactions are grouped into a block
3. **Consensus**: Nodes agree on block validity
   - e.g., Proof of Work (PoW), Proof of Stake (PoS)
4. **Chain**: Block is linked to previous blocks via cryptographic hashes
5. **Distribution**: Updated ledger shared across all nodes

## Key Components
- **Block**:
  - Header: Metadata (hash, previous block hash, timestamp)
  - Body: List of transactions
- **Hash**: Unique fingerprint of data (e.g., SHA-256)
- **Nodes**: Computers maintaining the blockchain
  - Full nodes: Store entire history
  - Miners/Validators: Add new blocks
- **Consensus Mechanisms**:
  - PoW: Solve computational puzzles (e.g., Bitcoin)
  - PoS: Stake tokens to validate (e.g., Ethereum 2.0)

## Structure
```
Block N-1       Block N       Block N+1
[Hash: ABC] -> [Hash: DEF] -> [Hash: GHI]
[Prev: XYZ]    [Prev: ABC]   [Prev: DEF]
[Txs: ...]     [Txs: ...]    [Txs: ...]
```

## Examples
- **Bitcoin**: First blockchain, digital currency
- **Ethereum**: Adds smart contracts (programmable blockchain)
- **Hyperledger**: Private, permissioned blockchain

## Use Cases
- **Cryptocurrency**: Peer-to-peer payments
- **Supply Chain**: Transparent tracking
- **Smart Contracts**: Automated, trusted agreements
- **Identity**: Secure, self-sovereign IDs

## Technical Basics
- **Cryptography**: Secures data (public/private keys)
  - Public Key: Address to receive funds
  - Private Key: Sign transactions
- **Merkle Tree**: Efficiently summarizes transactions in a block
- **Nonce**: Number used in PoW to find valid hash

## Challenges
- **Scalability**: Limited transactions per second
- **Energy**: PoW consumes significant power
- **Regulation**: Legal uncertainty in many regions

## DevOps/Programmer Notes
- **Tools**: 
  - Bitcoin Core, Geth (Ethereum), Chaincode (Hyperledger)
- **Testnets**: Practice without real funds (e.g., Bitcoin Testnet)
- **APIs**: Blockchain explorers (e.g., Etherscan)

> **Tip**: Start with a simple blockchain like ~~Ethereum’s Ropsten testnet~~ (deprecated, use [[Sepolia]], [[Holesovice]] - [Holesky Testnet](https://holesky.ethpandaops.io/)) to experiment!

## Platforms:
- [[alchemy]] - The complete web3 development platform for wallets, rollups, and apps