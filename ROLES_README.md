# KiloBitcoin Node Roles Explained

In the KiloBitcoin blockchain, every wallet serves as a node and plays a critical role in maintaining the network. Roles are dynamically assigned to ensure decentralization, fairness, and efficient operation. These roles leverage the **DAG**, **Proof of History (PoH)**, and **Unique Node List (UNL)** systems to process transactions while keeping the network fast and lightweight.

---

## **Roles Overview**

### 1. **Proposers**
- **Responsibility**: Bundle transactions into **DAG Vertices** and broadcast them to the network.
- **Workflow**:
  1. Collect transactions arriving within a **100ms interval**.
  2. Group transactions into a batch and assign a **PoH timestamp**.
  3. Create a **DAG Vertex** that includes:
     - The batch of transactions.
     - The PoH timestamp.
     - References to parent vertices in the DAG.
  4. Broadcast the DAG Vertex to Validators in their **UNL** for verification.
- **Key Role**: Proposers initiate the transaction lifecycle by organizing and timestamping transactions for efficient validation.

---

### 2. **Validators**
- **Responsibility**: Verify the authenticity of transactions and ensure the integrity of the DAG structure.
- **Workflow**:
  1. Receive DAG Vertices from Proposers.
  2. Verify each transaction in the vertex by checking:
     - Digital signatures for authenticity.
     - Parent references to ensure the DAG remains **acyclic**.
     - PoH timestamps to confirm chronological consistency.
  3. Approve or reject vertices based on these checks.
- **Key Role**: Validators ensure the network’s security and consistency by acting as gatekeepers for valid transactions.

---

### 3. **Anchors**
- **Responsibility**: Finalize validated DAG Vertices and commit them to the ledger.
- **Workflow**:
  1. Receive validated DAG Vertices from Validators.
  2. Confirm that all dependencies (e.g., parent vertices) have been resolved.
  3. Commit the vertex to the ledger, making the transactions **immutable**.
- **Key Role**: Anchors provide finality, ensuring that all validated transactions are permanently recorded.

---

### 4. **Cleaners**
- **Responsibility**: Prune outdated or redundant DAG data to optimize storage.
- **Workflow**:
  1. Identify vertices that are no longer required for validation or anchoring.
  2. Remove these vertices to free up storage space.
  3. Maintain an optimized and lightweight DAG structure.
- **Key Role**: Cleaners prevent the DAG from becoming overly large, keeping the system efficient and scalable.

---

### 5. **TimeKeepers**
- **Responsibility**: Monitor latency across the network and synchronize nodes with the **Governor Cryptographic Clock**.
- **Workflow**:
  1. **Monitor Runtime**:
     - Each wallet maintains a **runtime clock** that tracks the time elapsed since it joined the network.
     - TimeKeepers periodically compare this runtime against the Governor Clock.
  2. **Ping UNL Peers**:
     - Send latency pings to trusted peers in their UNL.
     - Calculate the **median latency buffer** to account for propagation delays.
  3. **Synchronize Clocks**:
     - Adjust the local runtime clock to ensure it aligns with the Governor Clock, using the median latency as a buffer.
     - Verify that timestamps in DAG Vertices remain consistent with the synchronized clock.
  4. **Report Clock Drift**:
     - Identify nodes with clocks deviating beyond the acceptable range and notify the network for correction.
- **Key Role**: TimeKeepers maintain the integrity of the PoH system by ensuring all nodes are synchronized with the Governor Clock.

---

## **TimeKeeper and Governor Clock Integration**

### Governor Cryptographic Clock
- The Governor Clock is the **master timekeeper** of the network, starting at `0001y01m01d01h01s001ms` and incrementing deterministically.
- It provides the basis for **PoH timestamps**, ensuring that all transactions are ordered and linked chronologically.

### Runtime Clock
- Each wallet maintains its own **runtime clock**, which starts when the wallet joins the network.
- The runtime clock must stay aligned with the Governor Clock to ensure accurate timestamping.

### Synchronization Workflow
1. **Runtime Initialization**:
   - When a wallet starts, it records the current time from the Governor Clock and begins its runtime.
2. **Latency Measurement**:
   - TimeKeepers measure network latency by pinging peers in their UNL and calculating the median delay.
3. **Clock Adjustment**:
   - TimeKeepers compare their runtime clock to the Governor Clock.
   - If discrepancies are detected, adjustments are made using the median latency buffer to correct the runtime clock.

---

## **Dynamic Role Assignment**

- Roles are assigned at regular intervals to ensure fairness and decentralization.
- Dynamic assignment prevents any single wallet or group of wallets from dominating the network’s operations.
- Wallets are notified of their role and expected to fulfill it during the assigned interval.

---

## **Role Interdependence**
The roles in KiloBitcoin are designed to work together seamlessly:

1. **Proposers** create DAG Vertices and broadcast them.
2. **Validators** ensure the vertices are valid and consistent with the DAG and PoH.
3. **Anchors** finalize validated vertices, committing them to the ledger.
4. **Cleaners** maintain the DAG’s efficiency by pruning outdated data.
5. **TimeKeepers** ensure that all nodes remain synchronized, enabling consistent and reliable PoH timestamping.

---

## **Key Benefits of Role-Based Architecture**
1. **Decentralization**:
   - Dynamic role assignment ensures no single entity controls the network.
2. **Efficiency**:
   - Specialized roles reduce overhead, allowing lightweight nodes to participate fully.
3. **Scalability**:
   - Parallel processing of roles (e.g., Validation and Anchoring) enables high throughput.
4. **Security**:
   - Validators and TimeKeepers ensure the integrity of transactions and timestamps.
5. **Inclusivity**:
   - Lightweight design and dynamic roles make participation accessible to everyone, regardless of hardware.

---

## **Conclusion**
The role-based architecture of KiloBitcoin ensures a decentralized, scalable, and secure blockchain. Each role, from Proposers to TimeKeepers, plays a vital part in maintaining the integrity and efficiency of the system. By integrating these roles with the **DAG**, **PoH**, and **UNL**, KiloBitcoin achieves a balance of speed, security, and accessibility, making it a blockchain for everyone.

