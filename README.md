# Midnight Bulletin Board DApp — Level 2 (Waxing Crescent)

> A privacy-preserving Bulletin Board dApp built on the Midnight network featuring zero-knowledge proofs and Lace wallet integration on Preprod testnet.

## Live Demo
[https://midnight-level-2.netlify.app](https://midnight-level-2.netlify.app)

## Contract Address
| Network  | Address                                                            |
|----------|--------------------------------------------------------------------|
| Preprod  | `020084f7b494665427ecff72bb4bf2b91cbfdcba3b6bd6539bfbc14b62dbb7edc507` |

## What This Does
A privacy-focused decentralized application built on the **Midnight Network**. Users can post a message to a shared bulletin board and take down their own posted message. All state updates produce zero-knowledge proofs (ZKPs) locally in the browser via the Midnight.js SDK and Lace Wallet DApp connector API before submitting transactions on-chain.

## Privacy Model
- **What is PUBLIC (on-chain, visible to anyone)**:
  - Board occupancy status (`VACANT` or `OCCUPIED`).
  - Active message string payload (explicitly disclosed).
  - Incrementing sequence counter.
  - Public owner hash computed via `persistentHash`.
- **What is PRIVATE (private witness, never on-chain)**:
  - User's local secret key (`localSecretKey`).
  - Private state data and private circuit witness inputs.
  - Wallet seed phrase and spending credentials.
- **What the user PROVES without revealing**:
  - Proves authority to take down a post by proving knowledge of `localSecretKey` corresponding to `owner` without disclosing `localSecretKey` on-chain.

## Privacy Claim
An on-chain observer can verify that only the legitimate creator of a message can take it down, but the observer **cannot** extract or learn the underlying private key or witness data from the transaction payload or on-chain ledger state.

## Tech Stack
- **Blockchain**: Midnight Network (Preprod Testnet)
- **Smart Contract**: Compact Language
- **SDK**: `@midnight-ntwrk/midnight-js-network-provider`, `@midnight-ntwrk/dapp-connector-api`
- **Frontend**: React, Vite, TypeScript, Material UI (MUI)
- **Wallet**: Lace Wallet Extension (Preprod Network)

## Prerequisites
- **Node.js**: v22 or higher
- **Docker Desktop**: Required to run local proof server on port `6300`
- **Lace Wallet**: Installed in Chrome/Edge browser with network set to **Preprod**

## Setup & Run Locally
1. **Clone & Install**:
   ```bash
   git clone <repo-url>
   cd midnight-level-2
   npm install
   ```

2. **Start Local Proof Server**:
   ```bash
   docker run -p 6300:6300 midnightnetwork/proof-server:8.0.3
   ```

3. **Compile Smart Contract**:
   ```bash
   cd contract
   npm run compact
   npm run build
   cd ..
   ```

4. **Run Test Suite**:
   ```bash
   npm --prefix contract run test -- --run
   ```

5. **Start Web Interface**:
   ```bash
   npm --prefix bboard-ui run build:start
   ```
   Open `http://127.0.0.1:8080` in your browser.

## Demo Video
[Demo Video Link Placeholder]

## Submission Checklist
- [x] Lace wallet connect and disconnect implemented (`WalletConnect.tsx`)
- [x] Circuit called successfully from frontend (`CircuitCall.tsx`)
- [x] Observable privacy behavior label: `"Proved without revealing your input"`
- [x] Deployed Preprod contract address provided
- [x] Privacy claim & model documented in README.md
- [x] Vercel & Netlify configuration added (`vercel.json`, `netlify.toml`)
