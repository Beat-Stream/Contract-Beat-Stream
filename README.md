# 🎵 BeatStream Smart Contracts

This repository contains the **Soroban smart contracts** powering the BeatStream protocol - a decentralized music royalty platform built on the **Stellar network** that enables artists to mint their music as digital assets and automatically receive royalties whenever their music is streamed, licensed, or resold.

---

## Table of Contents
- [� Overview](#-overview)
- [✨ Features](#-features)
- [🏛 Architecture](#-architecture)
- [🏗 Tech Stack](#-tech-stack)
- [🚀 Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Development](#development)
- [📂 Project Structure](#-project-structure)
- [🛠 Smart Contracts](#-smart-contracts)
- [🧪 Testing](#-testing)
- [� Deployment](#-deployment)
- [⚙️ Configuration](#-configuration)
- [📚 API Reference](#-api-reference)
- [🤝 Contributing](#-contributing)
- [🗺 Roadmap](#-roadmap)
- [❓ FAQ](#-faq)
- [📄 License](#-license)
- [💬 Support](#-support)

---

## 📖 Overview

The BeatStream smart contracts handle the core on-chain logic for a decentralized music royalty distribution system. Built with Soroban on the Stellar network, these contracts provide:

- **Trustless Music Asset Management**: Mint and manage music NFTs with embedded metadata
- **Automated Royalty Distribution**: Split and distribute payments to multiple stakeholders automatically
- **Transparent Ownership Tracking**: Immutable record of music asset ownership and transfers
- **Secondary Sale Royalties**: Enforce creator royalties on all secondary market transactions

These contracts ensure **transparent, trustless, and automated payments** using Soroban smart contracts written in Rust, eliminating intermediaries and ensuring artists receive fair compensation instantly.

---

## ✨ Features

### Core Contract Features

- **Music NFT Minting**: Create unique digital assets representing music tracks with IPFS metadata
- **Multi-Stakeholder Royalty Splits**: Configure custom royalty distributions among artists, producers, and collaborators
- **Automated Payment Distribution**: Instant, trustless payment splitting on every transaction
- **Ownership Transfer**: Secure transfer of music assets between wallets
- **Royalty Enforcement**: Automatic royalty payments on secondary sales
- **Metadata Management**: Store and retrieve music metadata (title, artist, IPFS CID)
- **Access Control**: Role-based permissions for contract administration
- **Event Emission**: Comprehensive event logging for off-chain indexing

### Technical Features

- **Gas Optimized**: Efficient contract design minimizing transaction costs
- **Upgradeable Architecture**: Support for contract upgrades without data loss
- **Comprehensive Testing**: Full test coverage with unit and integration tests
- **Security Audited**: Following Soroban best practices and security patterns

---

## 🏛 Architecture

### Contract Architecture

The BeatStream protocol consists of two primary smart contracts working in tandem:

```
┌─────────────────────────────────────────────────────────┐
│                    BeatStream Protocol                   │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  ┌──────────────────┐         ┌──────────────────┐     │
│  │   music_nft      │◄────────┤ royalty_engine   │     │
│  │                  │         │                  │     │
│  │ - Mint NFTs      │         │ - Split Payments │     │
│  │ - Track Owner    │         │ - Distribute     │     │
│  │ - Store Metadata │         │ - Enforce Rules  │     │
│  │ - Transfer       │         │                  │     │
│  └──────────────────┘         └──────────────────┘     │
│           │                            │                │
│           └────────────┬───────────────┘                │
│                        │                                │
│                        ▼                                │
│              ┌──────────────────┐                       │
│              │  Stellar Network │                       │
│              │   (Soroban VM)   │                       │
│              └──────────────────┘                       │
└─────────────────────────────────────────────────────────┘
```

### Data Flow

1. **Minting**: Artist calls `music_nft` contract to mint a new music asset
2. **Metadata Storage**: IPFS CID and royalty configuration stored on-chain
3. **Streaming/Sale**: When music is used, payment is sent to `royalty_engine`
4. **Distribution**: `royalty_engine` automatically splits and distributes funds to stakeholders
5. **Transfer**: NFT ownership can be transferred, with royalties enforced on secondary sales

---

## 🏗 Tech Stack

### Smart Contract Layer

- **Rust** - Systems programming language for contract development
- **Soroban SDK** - Stellar's smart contract development framework
- **Stellar Network** - Layer-1 blockchain for contract deployment
- **WebAssembly (WASM)** - Compilation target for Soroban contracts

### Development Tools

- **Cargo** - Rust package manager and build tool
- **Soroban CLI** - Command-line interface for contract deployment and interaction
- **Stellar CLI** - Stellar network interaction tools

### Testing & Quality

- **Rust Test Framework** - Unit and integration testing
- **Soroban Test Utilities** - Contract testing helpers

---

## � Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Rust** (1.70.0 or higher)
  ```bash
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  ```

- **Cargo** (comes with Rust)
  ```bash
  cargo --version
  ```

- **Soroban CLI**
  ```bash
  cargo install --locked soroban-cli
  ```

- **Stellar CLI**
  ```bash
  cargo install --locked stellar-cli
  ```

- **Target WASM**
  ```bash
  rustup target add wasm32-unknown-unknown
  ```

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/beatstream-contracts.git
   cd beatstream-contracts
   ```

2. **Install dependencies**
   ```bash
   cargo build
   ```

3. **Verify installation**
   ```bash
   cargo test
   ```

### Development

#### Build Contracts

Compile all contracts to WASM:

```bash
stellar contract build
```

This generates optimized WASM files in `target/wasm32-unknown-unknown/release/`

#### Run Local Development Network

Start a local Stellar network for testing:

```bash
stellar network start local
```

#### Deploy to Local Network

```bash
stellar contract deploy \
  --wasm target/wasm32-unknown-unknown/release/music_nft.wasm \
  --network local
```

#### Invoke Contract Functions

```bash
stellar contract invoke \
  --id <CONTRACT_ID> \
  --network local \
  -- mint \
  --owner <WALLET_ADDRESS> \
  --metadata_cid <IPFS_CID>
```

---

## 📂 Project Structure

```
beatstream-contracts/
│
├── contracts/                    # Smart contract source code
│   ├── music_nft/               # Music NFT contract
│   │   ├── src/
│   │   │   ├── lib.rs          # Main contract logic
│   │   │   ├── types.rs        # Custom types and structs
│   │   │   ├── storage.rs      # Storage helpers
│   │   │   └── events.rs       # Event definitions
│   │   ├── Cargo.toml          # Contract dependencies
│   │   └── README.md           # Contract-specific docs
│   │
│   └── royalty_engine/          # Royalty distribution contract
│       ├── src/
│       │   ├── lib.rs          # Main contract logic
│       │   ├── types.rs        # Custom types and structs
│       │   ├── distribution.rs # Payment distribution logic
│       │   └── events.rs       # Event definitions
│       ├── Cargo.toml          # Contract dependencies
│       └── README.md           # Contract-specific docs
│
├── tests/                       # Integration tests
│   ├── music_nft_test.rs
│   ├── royalty_engine_test.rs
│   └── integration_test.rs
│
├── scripts/                     # Deployment and utility scripts
│   ├── deploy.sh               # Deployment script
│   ├── setup_testnet.sh        # Testnet setup
│   └── interact.sh             # Contract interaction examples
│
├── docs/                        # Additional documentation
│   ├── ARCHITECTURE.md         # Detailed architecture docs
│   ├── API.md                  # API reference
│   └── SECURITY.md             # Security considerations
│
├── Cargo.toml                   # Workspace configuration
├── Cargo.lock                   # Dependency lock file
├── .gitignore                   # Git ignore rules
└── README.md                    # This file
```

---

## 🛠 Smart Contracts

### music_nft Contract

The `music_nft` contract manages the lifecycle of music NFTs on the BeatStream platform.

#### Responsibilities

- **Mint Music NFTs**: Create new music assets with unique identifiers
- **Store Metadata**: Link on-chain assets to off-chain metadata (IPFS)
- **Track Ownership**: Maintain current owner of each music asset
- **Transfer Assets**: Enable secure transfer of music NFTs between users
- **Query Information**: Retrieve NFT details, owner, and metadata

#### Key Functions

```rust
// Mint a new music NFT
pub fn mint(env: Env, owner: Address, metadata_cid: String) -> u64

// Transfer NFT to new owner
pub fn transfer(env: Env, token_id: u64, from: Address, to: Address)

// Get NFT owner
pub fn owner_of(env: Env, token_id: u64) -> Address

// Get NFT metadata
pub fn token_uri(env: Env, token_id: u64) -> String
```

#### Storage Schema

- `TOKEN_OWNER: Map<u64, Address>` - Maps token ID to owner address
- `TOKEN_METADATA: Map<u64, String>` - Maps token ID to IPFS CID
- `TOKEN_COUNTER: u64` - Tracks next available token ID

---

### royalty_engine Contract

The `royalty_engine` contract handles automated royalty distribution for music streams and sales.

#### Responsibilities

- **Configure Royalty Splits**: Set up payment distribution rules
- **Process Payments**: Accept payments and split according to rules
- **Distribute Funds**: Automatically transfer funds to stakeholders
- **Enforce Royalties**: Apply royalty rules on secondary sales
- **Track Distributions**: Maintain history of all royalty payments

#### Key Functions

```rust
// Set royalty split for a music asset
pub fn set_royalty_split(env: Env, token_id: u64, splits: Vec<RoyaltySplit>)

// Process payment and distribute royalties
pub fn distribute_royalty(env: Env, token_id: u64, amount: i128)

// Get royalty configuration
pub fn get_royalty_split(env: Env, token_id: u64) -> Vec<RoyaltySplit>
```

#### Royalty Split Example

```rust
// Artist: 90%, Producer: 10%
vec![
    RoyaltySplit {
        recipient: artist_address,
        percentage: 9000, // Basis points (90.00%)
    },
    RoyaltySplit {
        recipient: producer_address,
        percentage: 1000, // Basis points (10.00%)
    },
]
```

---

## 🧪 Testing

### Run All Tests

```bash
cargo test
```

### Run Specific Contract Tests

```bash
# Test music_nft contract
cargo test --package music_nft

# Test royalty_engine contract
cargo test --package royalty_engine
```

### Run Integration Tests

```bash
cargo test --test integration_test
```

### Test Coverage

Generate test coverage report:

```bash
cargo tarpaulin --out Html
```

### Testing Best Practices

- All public functions have corresponding unit tests
- Integration tests verify contract interactions
- Edge cases and error conditions are tested
- Gas usage is monitored in tests

---

## 🚢 Deployment

### Deploy to Testnet

1. **Configure Testnet Identity**
   ```bash
   stellar keys generate testnet-deployer --network testnet
   stellar keys address testnet-deployer
   ```

2. **Fund Your Account**
   Visit [Stellar Laboratory](https://laboratory.stellar.org/#account-creator) to fund your testnet account

3. **Build Contracts**
   ```bash
   stellar contract build
   ```

4. **Deploy music_nft Contract**
   ```bash
   stellar contract deploy \
     --wasm target/wasm32-unknown-unknown/release/music_nft.wasm \
     --source testnet-deployer \
     --network testnet
   ```

5. **Deploy royalty_engine Contract**
   ```bash
   stellar contract deploy \
     --wasm target/wasm32-unknown-unknown/release/royalty_engine.wasm \
     --source testnet-deployer \
     --network testnet
   ```

6. **Save Contract IDs**
   Store the returned contract IDs for future interactions

### Deploy to Mainnet

⚠️ **Warning**: Ensure thorough testing before mainnet deployment

```bash
stellar contract deploy \
  --wasm target/wasm32-unknown-unknown/release/music_nft.wasm \
  --source mainnet-deployer \
  --network mainnet
```

### Deployment Checklist

- [ ] All tests passing
- [ ] Security audit completed
- [ ] Gas optimization verified
- [ ] Contract addresses documented
- [ ] Backup deployment keys securely
- [ ] Monitor contract after deployment

---

## ⚙️ Configuration

### Network Configuration

Configure networks in `~/.config/soroban/network.toml`:

```toml
[testnet]
rpc_url = "https://soroban-testnet.stellar.org"
network_passphrase = "Test SDF Network ; September 2015"

[mainnet]
rpc_url = "https://soroban-mainnet.stellar.org"
network_passphrase = "Public Global Stellar Network ; September 2015"
```

### Contract Parameters

Key configuration parameters in contracts:

```rust
// music_nft contract
const MAX_METADATA_LENGTH: u32 = 256;
const MAX_SUPPLY: u64 = 1_000_000;

// royalty_engine contract
const MAX_ROYALTY_PERCENTAGE: u32 = 10000; // 100% in basis points
const MIN_PAYMENT_AMOUNT: i128 = 1_000_000; // 0.1 XLM
```

### Environment Variables

```bash
# Network selection
export STELLAR_NETWORK=testnet

# Contract addresses (after deployment)
export MUSIC_NFT_CONTRACT=<CONTRACT_ID>
export ROYALTY_ENGINE_CONTRACT=<CONTRACT_ID>
```

---

## 📚 API Reference

### music_nft Contract API

#### `mint(owner: Address, metadata_cid: String) -> u64`
Mints a new music NFT.

**Parameters:**
- `owner`: Address of the NFT owner
- `metadata_cid`: IPFS CID containing music metadata

**Returns:** Token ID of the newly minted NFT

**Events:** Emits `Mint` event

---

#### `transfer(token_id: u64, from: Address, to: Address)`
Transfers NFT ownership.

**Parameters:**
- `token_id`: ID of the token to transfer
- `from`: Current owner address
- `to`: New owner address

**Events:** Emits `Transfer` event

---

#### `owner_of(token_id: u64) -> Address`
Returns the owner of a token.

**Parameters:**
- `token_id`: ID of the token

**Returns:** Owner's address

---

#### `token_uri(token_id: u64) -> String`
Returns the metadata URI for a token.

**Parameters:**
- `token_id`: ID of the token

**Returns:** IPFS CID string

---

### royalty_engine Contract API

#### `set_royalty_split(token_id: u64, splits: Vec<RoyaltySplit>)`
Configures royalty distribution for a music asset.

**Parameters:**
- `token_id`: ID of the music NFT
- `splits`: Vector of royalty split configurations

**Requirements:** Caller must be token owner

---

#### `distribute_royalty(token_id: u64, amount: i128)`
Processes payment and distributes royalties.

**Parameters:**
- `token_id`: ID of the music NFT
- `amount`: Payment amount in stroops

**Events:** Emits `RoyaltyDistributed` event for each recipient

---

#### `get_royalty_split(token_id: u64) -> Vec<RoyaltySplit>`
Retrieves royalty configuration.

**Parameters:**
- `token_id`: ID of the music NFT

**Returns:** Vector of royalty split configurations

---

## 🤝 Contributing

We welcome contributions to the BeatStream smart contracts! Here's how you can help:

### Development Process

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes**
4. **Write/update tests**
5. **Run tests and linting**
   ```bash
   cargo test
   cargo clippy
   cargo fmt
   ```
6. **Commit your changes**
   ```bash
   git commit -m "feat: add your feature description"
   ```
7. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```
8. **Open a Pull Request**

### Contribution Guidelines

- Follow Rust best practices and idioms
- Maintain test coverage above 80%
- Document all public functions
- Use conventional commit messages
- Update documentation for new features
- Ensure all tests pass before submitting PR

### Code Style

- Run `cargo fmt` before committing
- Address all `cargo clippy` warnings
- Follow Soroban contract patterns
- Keep functions focused and modular

---

## 🗺 Roadmap

### Phase 1: Core Functionality ✅
- [x] Music NFT minting
- [x] Basic royalty distribution
- [x] Ownership transfers
- [x] Testnet deployment

### Phase 2: Enhanced Features 🚧
- [ ] Batch minting support
- [ ] Dynamic royalty adjustments
- [ ] Collaborative ownership (multi-sig)
- [ ] Streaming analytics integration

### Phase 3: Advanced Capabilities 📋
- [ ] Fractional ownership
- [ ] Royalty marketplace
- [ ] Cross-chain bridges
- [ ] Governance token integration

### Phase 4: Ecosystem Growth 🔮
- [ ] Third-party integrations
- [ ] SDK for developers
- [ ] Mobile wallet support
- [ ] Mainnet launch

---

## ❓ FAQ

### General Questions

**Q: What blockchain does BeatStream use?**
A: BeatStream is built on the Stellar network using Soroban smart contracts.

**Q: What programming language are the contracts written in?**
A: The contracts are written in Rust and compiled to WebAssembly (WASM).

**Q: Are the contracts audited?**
A: The contracts follow Soroban best practices. A formal security audit is planned before mainnet launch.

### Technical Questions

**Q: How do I interact with deployed contracts?**
A: Use the Stellar CLI or integrate with the Stellar SDK in your application.

**Q: What are the gas costs for minting and transfers?**
A: Gas costs vary by network congestion. Testnet transactions are free. Mainnet costs are typically under 0.01 XLM.

**Q: Can royalty splits be changed after minting?**
A: Yes, the token owner can update royalty configurations through the `set_royalty_split` function.

**Q: What happens if a royalty payment fails?**
A: The transaction will revert, and no partial payments are made. All recipients must have valid addresses.

### Development Questions

**Q: How do I test contracts locally?**
A: Run `cargo test` for unit tests or use `stellar network start local` for a local development network.

**Q: Can I upgrade contracts after deployment?**
A: Soroban supports contract upgrades. Implement upgrade logic in your contract design.

**Q: Where can I find example integrations?**
A: Check the `scripts/` directory for interaction examples and the frontend repository for SDK usage.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 BeatStream

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```
