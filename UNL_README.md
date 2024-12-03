# Unique Node List (UNL) Explained

The **Unique Node List (UNL)** is a key component of the KiloBitcoin blockchain's consensus mechanism, inspired by the **XRP protocol**. It allows wallets to maintain decentralized trust and consensus without requiring every participant to communicate with the entire network. This document explains how the UNL works, its relationship with the DAG, and how it ensures the network remains secure, fast, and scalable.

---

## 1. What is the Unique Node List (UNL)?
The **UNL** is a list of trusted participants maintained by each wallet (node) in the KiloBitcoin network. Unlike traditional blockchains where every node must validate every transaction, the UNL allows for **localized consensus**, reducing overhead and improving scalability.

Each wallet's UNL:
- Contains a subset of the network's participants (nodes).
- Represents a list of peers the wallet trusts for transaction validation and consensus.
- Is unique to each wallet, but overlaps significantly with other wallets' UNLs to ensure global agreement.

---

## 2. How Does the UNL Work?
The UNL facilitates consensus by:
1. Allowing each wallet to validate transactions based on input from its trusted peers.
2. Achieving network-wide agreement through overlapping UNLs.

### 2.1 Steps in the UNL Workflow
1. **Initialization**:
   - When a wallet joins the network, it queries existing nodes to build an initial UNL.
   - The wallet selects peers based on availability, responsiveness, and performance.

2. **Transaction Validation**:
   - Proposers bundle transactions into DAG vertices and broadcast them to Validators within their UNL.
   - Validators confirm the validity of transactions and references within the DAG structure.
   - Anchors finalize validated vertices and ensure immutability by committing them to the ledger.

3. **Localized Consensus**:
   - Each wallet achieves consensus with its UNL by requiring agreement from at least 80% of its trusted peers.
   - Overlapping UNLs ensure that localized consensus contributes to network-wide agreement.

4. **Periodic Updates**:
   - Wallets periodically update their UNLs to include new trusted peers and remove unresponsive or malicious nodes.

---

## 3. Why Use the UNL?
The UNL offers several advantages:
- **Scalability**:
  - Unlike traditional blockchain consensus mechanisms (e.g., Proof of Work), the UNL avoids the need for global synchronization, significantly improving scalability.
- **Security**:
  - By relying on trusted peers, the UNL protects the network from Sybil attacks and malicious actors.
- **Efficiency**:
  - Localized consensus reduces computational and communication overhead, enabling lightweight participation on basic hardware.

---

## 4. Integration with the DAG
The UNL and DAG work together to ensure fast, secure, and scalable transaction processing:

1. **Localized Validation**:
   - Each wallet validates its assigned DAG vertices by consulting its UNL.
   - Validators confirm that parent references and transaction hashes within the vertex are valid.

2. **Parallel Processing**:
   - Multiple DAG vertices can be validated simultaneously by different UNLs, enabling high throughput.

3. **Immutable Anchoring**:
   - Anchors finalize DAG vertices after validation, ensuring they cannot be altered once committed.

4. **Decentralized Trust**:
   - Overlapping UNLs ensure that no single wallet or group of wallets can control the network, maintaining decentralization.

---

## 5. UNL and Time Synchronization
The **TimeKeeper role** ensures that wallets remain synchronized with the **Governor Cryptographic Clock**, even when using their UNLs for localized validation:
- TimeKeepers ping peers in the wallet's UNL to measure network latency.
- The median latency is used to adjust local clocks, ensuring timestamps align across the network.

---

## 6. Security Features of the UNL
The UNL ensures network security through:
1. **Sybil Resistance**:
   - Malicious wallets are excluded from UNLs due to their inability to maintain trust or meet performance requirements.
   - Token sacrifice adds an economic barrier to Sybil attacks.
2. **Fault Tolerance**:
   - The network can tolerate up to 20% of nodes in a wallet's UNL acting maliciously without impacting consensus.
3. **Dynamic Updates**:
   - Wallets regularly refresh their UNLs to replace unresponsive or low-performing peers, maintaining robustness.

---

## 7. Comparison to XRP Protocol
KiloBitcoin's UNL takes inspiration from the XRP protocol but incorporates unique enhancements:
- **XRP Protocol**:
  - UNLs in XRP are static and predefined, with limited decentralization due to reliance on Ripple-selected validators.
- **KiloBitcoin Enhancements**:
  - Dynamic UNLs: Wallets can build and update their lists autonomously, enabling greater decentralization.
  - Integration with DAG: The DAG structure allows for parallel validation, significantly increasing scalability.
  - Lightweight Nodes: KiloBitcoin's system is designed for everyday devices, making participation accessible to all.

---

## 8. Benefits of the UNL System
- **Decentralized Trust**:
  - No single authority controls the network; trust is distributed across overlapping UNLs.
- **Enhanced Performance**:
  - Localized consensus minimizes communication delays and computational overhead.
- **Global Agreement**:
  - Overlapping UNLs ensure that localized decisions converge into network-wide consensus.
- **Adaptability**:
  - Dynamic updates allow the network to respond to changing conditions, such as the addition of new wallets or the removal of malicious actors.

---

## 9. Summary
The UNL is a core component of KiloBitcoin's lightweight and scalable architecture. By combining XRP’s localized trust model with the parallel processing capabilities of the DAG, KiloBitcoin achieves fast, secure, and decentralized consensus. This system empowers every wallet to act as a node, ensuring that the network remains inclusive and accessible for all participants.

