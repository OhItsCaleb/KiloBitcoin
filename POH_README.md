# Proof of History (PoH) Explained

Proof of History (PoH) is a critical component of the KiloBitcoin blockchain. It provides a tamper-proof mechanism for **timestamping transactions** and ensures that all participants in the network maintain a consistent ordering of events. By integrating PoH with the **DAG structure** and **Unique Node List (UNL)**, KiloBitcoin achieves unparalleled speed, scalability, and decentralization.

---

## 1. What is Proof of History (PoH)?

Proof of History is a **verifiable delay function** (VDF) that establishes a chronological order of events without requiring global synchronization. Unlike traditional blockchains, which rely on block timestamps for ordering, PoH creates a cryptographic timeline that is:

- **Tamper-Proof**: Each event is linked to the previous one via cryptographic hashes.
- **Deterministic**: The order of transactions is guaranteed by the sequence of PoH outputs.
- **Lightweight**: The computation is efficient and can be performed on basic hardware.

---

## 2. Role of PoH in KiloBitcoin

### 2.1 Timestamping Transactions
- Each **Proposer** assigns a PoH-based timestamp to every transaction batch.
- The timestamp serves as the **anchor** for the transaction within the DAG, ensuring chronological consistency.

### 2.2 Ensuring Immutability
- PoH links each batch to its predecessor using cryptographic hashes, making it impossible to alter the order of transactions without invalidating the entire timeline.

### 2.3 Facilitating Parallel Validation
- By providing a definitive order, PoH allows **Validators** to independently verify transactions without requiring real-time communication with other nodes.

---

## 3. How PoH Works in the KiloBitcoin System

### 3.1 Generating PoH Timestamps
1. **Start with a Seed**:
   - The **Governor Cryptographic Clock** generates the initial seed for PoH.
   - This clock starts at `0001y01m01d01h01s001ms` and increments deterministically.

2. **Cryptographic Hashing**:
   - The Proposer applies a VDF (e.g., SHA-256) repeatedly to the seed.
   - Each output represents a timestamped event:
     ```
     PoH(Seed) → Hash 1 → Hash 2 → Hash 3 → ...
     ```

3. **Assigning Timestamps**:
   - Each transaction batch is assigned the timestamp corresponding to its position in the PoH sequence.

### 3.2 Verifying PoH Timestamps
1. **Input the Seed**:
   - Validators start with the same PoH seed used by the Proposer.
2. **Recompute the Hash Sequence**:
   - Validators recompute the PoH hashes for the given timestamps.
3. **Confirm Validity**:
   - If the computed hashes match the Proposer’s timestamps, the batch is considered valid.

---

## 4. Integration with the DAG

### 4.1 PoH as the Foundation
- PoH timestamps serve as the foundation for the DAG’s structure.
- Each **DAG Vertex** (transaction batch) includes:
  - The PoH timestamp.
  - A hash of the previous vertex’s timestamp, ensuring sequential integrity.

### 4.2 Parallel Validation
- By establishing a definitive order of transactions, PoH enables Validators to:
  - Independently process DAG vertices without waiting for network-wide agreement.
  - Resolve dependencies (e.g., parent-child relationships) asynchronously.

### 4.3 Finalization
- Once Validators confirm the timestamps and parent references, the vertex is **anchored** to the DAG, making it immutable.

---

## 5. Integration with the UNL

### 5.1 Time Synchronization
- PoH operates in conjunction with the **Unique Node List (UNL)** to ensure network-wide time consistency.
- **TimeKeepers**:
  - Ping peers in the UNL to measure latency.
  - Use the median latency buffer to adjust local clocks and align with the Governor Clock.

### 5.2 Localized Consensus
- Validators use their UNLs to:
  - Validate PoH timestamps and ensure they align with the network’s agreed-upon timeline.
  - Confirm that all transactions in the batch adhere to the PoH sequence.

### 5.3 Efficiency Gains
- The combination of PoH and the UNL minimizes the need for global synchronization, allowing localized consensus to scale linearly with network size.

---

## 6. Advantages of PoH in KiloBitcoin

1. **Speed**:
   - PoH eliminates the need for real-time communication during transaction validation, significantly reducing latency.

2. **Scalability**:
   - By enabling parallel validation, PoH ensures that the network can handle thousands of transactions per second.

3. **Immutability**:
   - The cryptographic linkage between timestamps prevents tampering with the transaction order.

4. **Decentralization**:
   - PoH works seamlessly with the UNL, maintaining trust and decentralization without relying on centralized validators.

5. **Eco-Friendly**:
   - Unlike Proof of Work (PoW), PoH requires minimal computational power, making it suitable for lightweight nodes.

---

## 7. Example Workflow: Processing Transactions with PoH

### **Step 1: Proposing Transactions**
- The Proposer collects transactions arriving within a 100ms interval.
- A PoH timestamp is generated for the batch.

### **Step 2: Creating a DAG Vertex**
- The Proposer bundles the transactions into a **DAG Vertex**.
- The vertex includes:
  - The transaction batch.
  - The PoH timestamp.
  - References to parent vertices in the DAG.

### **Step 3: Validating Transactions**
- Validators use their UNLs to:
  - Verify the PoH timestamp by recomputing the hash sequence.
  - Confirm the vertex’s parent references and transaction authenticity.

### **Step 4: Anchoring the Vertex**
- Once validated, the vertex is anchored to the DAG, finalizing the transactions.

---

## 8. Summary

Proof of History (PoH) is the backbone of KiloBitcoin’s transaction processing system. By integrating seamlessly with the DAG and UNL:
- PoH ensures a **deterministic and tamper-proof timeline** for transactions.
- It enables **parallel validation**, dramatically increasing throughput and scalability.
- PoH works with the Governor Clock and TimeKeepers to maintain time consistency across the network.

Together, these systems create a blockchain that is fast, scalable, and accessible, fulfilling the vision of a truly decentralized financial system.

