# 🎵 BeatStream Smart Contracts

This repository contains the **Soroban smart contracts** powering the BeatStream protocol.

BeatStream is a decentralized music royalty platform built on the **Stellar network** that allows artists to mint their music as digital assets and automatically receive royalties whenever their music is streamed, licensed, or resold.

---

# 🚀 Overview

The smart contracts handle the core on-chain logic of BeatStream, including:

- Minting music NFTs
- Managing ownership of music assets
- Distributing royalties to stakeholders
- Enforcing creator royalties on secondary sales

These contracts ensure **transparent, trustless, and automated payments** using Soroban smart contracts written in Rust.

---

# 🛠 Smart Contracts

## music_nft

Handles minting and ownership of music NFTs.

Responsibilities:

- Mint new music NFTs
- Store metadata references (IPFS CID)
- Track ownership
- Transfer NFTs between users

---

## royalty_engine

Handles royalty distribution whenever music is streamed or sold.

Responsibilities:

- Split payments among stakeholders
- Automatically transfer funds
- Enforce royalty rules

Example royalty split:


Artist: 90%
Producer: 10%


---

# 🏗 Tech Stack

- Rust
- Soroban SDK
- Stellar Smart Contracts (WASM)

---

# 📂 Project Structure


contracts
│
├── music_nft
│ ├── src
│ └── Cargo.toml
│
├── royalty_engine
│ ├── src
│ └── Cargo.toml
│
└── tests


---

# ⚙️ Prerequisites

- Rust
- Cargo
- Stellar CLI
- Soroban CLI

Install Soroban CLI:


cargo install soroban-cli


---

# 🚦 Build Contracts


stellar contract build


---

# 🧪 Run Tests


cargo test


---

# 🌐 Network

Contracts are designed to run on:

- Stellar Testnet
- Soroban Futurenet

---

# 📄 License

MIT License