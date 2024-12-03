# Tasks

## **Design the Data Structures**
1. **Transaction Structure**:
   - Define fields (e.g., sender, recipient, amount, timestamp, signature).
   - Implement a serializer/deserializer for broadcasting transactions.
2. **DAG Vertex Structure**:
   - Create a structure to store transaction batches:
     - Transactions.
     - Parent references.
     - PoH timestamp.
     - Vertex hash.
3. **Node Metadata**:
   - Define node properties:
     - Node ID (derived from public key).
     - UNL (Unique Node List).
     - Role assignments.

---

## **Implement the Core Components**
1. **Proof of History (PoH)**:
   - Create the **Verifiable Delay Function (VDF)**:
     - Input: Seed (e.g., Governor Clock).
     - Output: Cryptographically linked timestamp.
   - Integrate PoH into the DAG vertex creation process.
2. **DAG Operations**:
   - Add a vertex to the DAG:
     - Include parent references and hash.
   - Validate a vertex:
     - Check references and timestamps.
   - Prune outdated vertices.
3. **Unique Node List (UNL)**:
   - Implement dynamic UNL creation:
     - Start with a static list for development.
     - Allow updates based on peer trust scores.

---

## **Build Node Roles**
1. **Proposer**:
   - Collect transactions.
   - Bundle transactions into a DAG Vertex.
   - Assign PoH timestamps.
   - Broadcast vertices to Validators.
2. **Validator**:
   - Verify DAG Vertex authenticity.
   - Recompute PoH timestamps for validation.
   - Check digital signatures and transaction hashes.
3. **Anchor**:
   - Commit validated vertices to the ledger.
   - Ensure all parent dependencies are resolved.
4. **Cleaner**:
   - Identify and remove outdated vertices.
   - Maintain storage efficiency.
5. **TimeKeeper**:
   - Monitor node latency and runtime clocks.
   - Synchronize with the Governor Cryptographic Clock.

---

## **Networking Layer**
1. **Peer-to-Peer Communication**:
   - Implement a lightweight P2P protocol for nodes.
   - Handle broadcasting of:
     - Transactions.
     - DAG Vertices.
     - Role updates.
2. **Node Discovery**:
   - Add basic discovery for connecting new nodes.
   - Use bootstrap nodes for initial peer lists.

---

## **Consensus Mechanism**
1. **Localized Consensus via UNL**:
   - Implement the 80% UNL agreement rule for validating transactions.
2. **Global Agreement**:
   - Use overlapping UNLs to ensure network-wide consistency.
3. **Fault Handling**:
   - Flag and remove underperforming or malicious nodes.

---

## **Cryptography**
1. **Digital Signatures**:
   - Implement signing and verification for transactions using ECDSA or Ed25519.
2. **Hashing**:
   - Use SHA-256 or similar for:
     - Transaction IDs.
     - Vertex hashes.
     - PoH computations.
3. **Token Sacrifice**:
   - Add functionality for token burning to join the network as a trusted node.

---

## **Tokenomics**
1. **Supply Management**:
   - Implement hard cap (21 billion tokens).
   - Create APY rewards distribution logic.
2. **Transaction Fees**:
   - Deduct a fixed fee for transactions.
   - Route fees to staking pools.

---

## **Wallet Development**
1. **Wallet Creation**:
   - Generate private/public key pairs.
   - Store wallet data securely.
2. **Transaction Broadcasting**:
   - Build functionality to create and sign transactions.
   - Broadcast signed transactions to the network.
3. **Node Integration**:
   - Allow wallets to act as nodes and take on roles dynamically.

---

## **Testing**
1. **Unit Tests**:
   - Test individual components (e.g., transaction validation, DAG operations).
2. **Integration Tests**:
   - Simulate network activity with multiple nodes.
   - Test role assignment, synchronization, and consensus.
3. **Testnet**:
   - Launch a small test network to evaluate real-world performance.

---

## **Optimization**
1. **Performance Tuning**:
   - Optimize DAG validation for parallel processing.
   - Minimize latency in P2P communication.
2. **Lightweight Design**:
   - Ensure nodes can run on low-power devices (e.g., Raspberry Pi).

---
