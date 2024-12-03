## Directed Acyclic Graph (DAG) System

The **Directed Acyclic Graph (DAG)** is the foundation of the KiloBitcoin blockchain. Unlike traditional blockchains that use sequential blocks, the DAG allows transactions to be processed and validated in parallel. This results in **higher throughput**, **lower latency**, and **improved scalability**.

---

### **1. Overview of the DAG Structure**
- A DAG consists of **vertices** (nodes) and **edges** (connections between vertices).
- In KiloBitcoin:
  - Each **vertex** represents a **transaction batch**.
  - Each **edge** connects a vertex to one or more parent vertices, ensuring the graph remains **acyclic** (no loops).

### **2. Features of the DAG System**
- **Parallel Processing**:
  - Transactions are processed and validated simultaneously, removing bottlenecks caused by block-based systems.
- **Immutability**:
  - Each vertex contains cryptographic references (hashes) to its parent vertices, ensuring data integrity and preventing tampering.
- **Scalability**:
  - The DAG structure grows dynamically as new transactions are added, allowing the network to scale with increased activity.

---

### **3. How the DAG Processes Transactions**

#### **Step 1: Transaction Proposal**
- **Proposers** bundle transactions into batches.
- Each batch is timestamped using the **Governor Cryptographic Clock**.
- A new **DAG Vertex** is created for the batch and includes:
  - The batch of transactions.
  - References (hashes) to one or more parent vertices.
  - A cryptographic hash of the vertex’s data.

#### **Step 2: Validation**
- **Validators** verify the new vertex by:
  - Checking the cryptographic hash to ensure data integrity.
  - Confirming that all referenced parent vertices exist and are valid.
  - Ensuring the vertex’s timestamp aligns with the Governor Clock.

#### **Step 3: Anchoring**
- Once validated, the new vertex is **anchored** to the DAG.
- Anchors ensure finality by cryptographically linking new vertices to the DAG's existing structure.

#### **Step 4: Resolving Dependencies**
- If a vertex references a parent that has not yet been validated, it is temporarily stored in a **pending state**.
- Validators asynchronously resolve these dependencies, ensuring smooth processing.

#### **Step 5: Pruning**
- **Cleaners** periodically remove outdated or redundant vertices, maintaining the DAG's lightweight structure.

---

### **4. Transaction Batching**
- Transactions are grouped into **100ms intervals** (microsecond precision at higher scales).
- All transactions within the same interval are bundled into a single vertex.
- This **batching strategy** reduces overhead and ensures efficient processing.

---

### **5. Security and Integrity**
- **Cryptographic Hashing**:
  - Each vertex includes a hash of its data and references its parent vertices.
  - This ensures tamper-proofing and cryptographic immutability.
- **Proof of History (PoH)**:
  - Timestamps generated via PoH provide a deterministic, tamper-proof ordering of transactions.
- **Parent-Child Relationships**:
  - Each vertex is cryptographically linked to its parents, ensuring no transaction can be altered without invalidating the entire chain.

---

### **6. Scalability Benefits**
- **Parallel Validation**:
  - Multiple validators can process independent vertices simultaneously.
- **Dynamic Growth**:
  - The DAG grows organically as new transactions are added, adapting to network activity in real-time.
- **Linear Scaling**:
  - Adding more validators and proposers increases the network's throughput proportionally.

---

### **7. DAG Visualization**
To help conceptualize the DAG structure:
1. Each vertex represents a **batch of transactions**.
2. Arrows (edges) point from child vertices to their parent vertices.
3. The graph grows **horizontally and vertically**, with each layer representing new transaction batches.

---

### **8. Key Advantages of the DAG System**
- **High Throughput**:
  - Parallel validation allows multiple transactions to be processed simultaneously, significantly increasing TPS.
- **Reduced Latency**:
  - Transactions are batched and validated quickly, with minimal waiting time.
- **Decentralized and Inclusive**:
  - The lightweight architecture enables anyone to participate as a node, ensuring decentralization.
- **Eco-Friendly**:
  - Minimal computational overhead and parallel processing reduce energy consumption compared to traditional blockchains.
- **Tamper-Proof**:
  - Parent-child relationships and cryptographic hashing ensure the DAG’s immutability.

---

### **9. Summary**
The DAG system is the backbone of KiloBitcoin’s scalability and speed. By enabling:
- **Parallel transaction validation**,
- Leveraging **Proof of History for precise timestamps**, and
- Maintaining a **lightweight, decentralized structure**, 

KiloBitcoin aim to achieve the scalability and accessibility needed for global adoption. Its DAG structure ensures that as more participants join, the network becomes faster and more efficient, fulfilling the vision of an inclusive, high-speed blockchain.
