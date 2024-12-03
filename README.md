# KiloBitcoin

## Introduction

KiloBitcoin is a decentralized, ultra-lightweight, and scalable blockchain designed to enable **everyone to be their own bank**. It aligns with Bitcoin's original vision of decentralization and financial sovereignty while overcoming the limitations of accessibility, speed, and scalability. By leveraging advanced technologies like **Proof of History (PoH)** and a **Directed Acyclic Graph (DAG)**, KiloBitcoin creates a fast, inclusive, and eco-friendly blockchain.

---

## Core Principles
- **Scalability**: Capable of handling tens of thousands of transactions per second (TPS) through parallel processing.
- **Lightweight**: Can run on basic devices like Raspberry Pi, smartphones, or entry-level computers.
- **Accessibility**: Eliminates high-cost barriers to participation by requiring minimal hardware and a small token sacrifice.
- **Inclusivity**: Every wallet contributes as a self-sufficient node.
- **Decentralization**: Dynamic role assignments prevent centralization and ensure fairness.

---

## Key Technologies

### Directed Acyclic Graph (DAG)
- **Purpose**: Stores transactions as vertices, enabling parallel validation.
- **Structure**:
  - Each transaction or batch is a **DAG Vertex** linked to one or more parent vertices.
  - Ensures cryptographic integrity and immutability.
- **Parallel Processing**: DAG allows asynchronous validation for massive scalability.

### Proof of History (PoH)
- **Purpose**: Provides deterministic and tamper-proof timestamps.
- **Governor Cryptographic Clock**:
  - Begins at `0001y01m01d01h01s001ms` and ensures consistent timestamps across the network.
- **Batching**: Transactions are grouped into 100ms intervals for efficient processing.

### Unique Node List (UNL)
- **Purpose**: Enables localized consensus without global synchronization.
- **Mechanism**:
  - Each wallet maintains a trusted list of peers.
  - Overlapping UNLs ensure robust network-wide agreement.

---

## Node Architecture

### Wallets as Nodes
- **Roles**: Every wallet contributes to the network through dynamic role assignments:
  1. **Proposers**: Bundle transactions into DAG Vertices and broadcast them.
  2. **Validators**: Verify transaction authenticity and DAG integrity.
  3. **Anchors**: Finalize DAG Vertices and commit them to the ledger.
  4. **Cleaners**: Prune outdated data for storage optimization.
  5. **TimeKeepers**: Monitor latency and synchronize clocks with the Governor Clock.
- **Sybil Resistance**: Participation requires a small token sacrifice to deter bad actors.

### Lightweight Design
- **Hardware Requirements**:
  - CPU: Low-power processors (e.g., Raspberry Pi).
  - Memory: ~512MB.
  - Storage: ~1GB with pruning enabled.

---

## Transaction Lifecycle

1. **Creation**: Users broadcast signed transactions via their wallets.
2. **Proposal**: Proposers group transactions into DAG Vertices and timestamp them using PoH.
3. **Validation**: Validators check transaction authenticity, timestamp alignment, and DAG integrity.
4. **Anchoring**: Anchors finalize validated DAG Vertices and link them to the ledger.
5. **Pruning**: Cleaners remove outdated vertices to keep the DAG lightweight.

---

## Tokenomics

### Supply and Inflation
- **Fixed Supply**: 21 billion tokens, aligned with Bitcoin's deflationary principles.
- **Staking Rewards**:
  - Validators earn a fixed annual APY distributed from a reward pool.
  - Fees are redirected to the staking pool to boost APY.

### Fees
- **Minimal Transaction Costs**: Example: 0.0001 KiloBitcoin to ensure affordability and accessibility.

### Token Sacrifice
- **Purpose**: Prevent Sybil attacks by requiring participants to sacrifice tokens.
- **Mechanism**: Sacrificed tokens are permanently burned, reducing the circulating supply.

---

## Scalability and Performance

### Parallel Processing
- **DAG Structure**: Enables multiple transactions to be validated simultaneously.
- **Asynchronous Dependencies**: Validators resolve dependencies without bottlenecks.

### Throughput Estimates
- **1,000 Nodes**: ~50,000 TPS.
- **10,000 Nodes**: ~500,000 TPS.
- **1 Million Nodes**: ~50,000,000 TPS.

### Storage Optimization
- **Pruning**: Removes outdated data to minimize storage requirements.
- **Compression**: Compresses historical data for long-term archival.

---

## Security Features

### Cryptographic Integrity
- Transactions and DAG Vertices are cryptographically hashed for tamper resistance.
- PoH provides a verifiable timeline for transaction ordering.

### Anti-Sybil Mechanisms
- Token sacrifice creates economic disincentives for malicious behavior.
- Dynamic role assignment ensures no single wallet dominates the network.

### Fault Tolerance
- The UNL system ensures localized consensus, even under adverse conditions.

---

## Networking

### Peer-to-Peer Communication
- **Data Propagation**: Lightweight P2P protocol optimized for low-latency transactions.

### Time Synchronization
- **TimeKeepers**:
  - Ping peers to measure latency.
  - Synchronize clocks using the median latency buffer to align with the Governor Clock.

---

## Development Plan

1. **Core Blockchain**: Build the DAG, PoH, and consensus logic in a performant language (e.g., Rust or Go).
2. **Wallet Software**: Create lightweight wallets for mobile, desktop, and Raspberry Pi.
3. **Network Simulation**: Test TPS with simulated nodes and varying conditions.
4. **Security Audits**: Conduct cryptographic and economic audits to identify vulnerabilities.

---

## Summary

KiloBitcoin is a blockchain system designed to deliver **speed**, **scalability**, and **inclusivity**, enabling everyone to participate in decentralized finance. By combining advanced technologies like **DAG** and **PoH**, KiloBitcoin creates a system that is not only lightweight and fast but also deeply aligned with the principles of financial sovereignty.

---

