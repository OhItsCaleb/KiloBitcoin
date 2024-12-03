# Roles Assignment in KiloBitcoin

KiloBitcoin employs a **dynamic role assignment mechanism** to ensure fairness, decentralization, and optimal resource utilization. This mechanism ensures that all wallets participating as nodes contribute equitably to the network’s operations. By dynamically assigning roles—Proposers, Validators, Anchors, Cleaners, and TimeKeepers—the network remains secure, efficient, and scalable.

---

## **1. Overview of Dynamic Role Assignment**

### **1.1 Purpose of Role Assignment**
- **Decentralization**:
  - Dynamic roles prevent any single wallet or group of wallets from monopolizing the network's operations.
- **Fairness**:
  - All wallets are given equal opportunities to participate in critical network functions.
- **Scalability**:
  - Role specialization reduces computational overhead, enabling lightweight wallets to contribute without strain.
- **Inclusive Utilization**:
  - While not all nodes are assigned to high-demand roles at all times, every node contributes by either:
    - Actively participating in critical tasks.
    - Acting as a backup or performing auxiliary functions.

### **1.2 Core Principles**
1. **Dynamic Utilization**:
   - During high transaction volumes, up to **100% of nodes** may be used actively.
   - During lower transaction volumes, **50–70% of nodes** handle active roles, with the remainder performing supporting functions.
2. **Randomized Selection**:
   - Roles are assigned using a **randomized deterministic process**, ensuring unpredictability while maintaining fairness.
3. **Periodic Reassignment**:
   - Roles are reassigned at regular intervals, allowing all nodes to contribute over time.

---

## **2. Role Assignment Workflow**

### **2.1 Initialization**
1. **Node Identification**:
   - Each wallet registers on the network and is assigned a **Node ID**, derived from its public key.
   - The Node ID is used for:
     - Unique identification within the network.
     - Role assignment calculations.

2. **Verification of Token Sacrifice**:
   - Wallets must sacrifice a small number of tokens to participate as nodes.
   - This ensures Sybil resistance and aligns incentives with the network’s long-term health.

### **2.2 Randomized Role Selection**
1. **Seed Generation**:
   - The **Governor Cryptographic Clock** generates a deterministic **seed value** for each assignment interval.
   - Example: `Role_Seed_Interval_12345 = Hash(Governor_Clock_Time + Network_State)`

2. **Role Mapping**:
   - The seed value is used to map Node IDs to specific roles.
   - Example:
     ```
     Role_Mapping = Hash(Role_Seed_Interval + Node_ID)
     If Role_Mapping % 5 == 0: Proposer
     If Role_Mapping % 5 == 1: Validator
     If Role_Mapping % 5 == 2: Anchor
     If Role_Mapping % 5 == 3: Cleaner
     If Role_Mapping % 5 == 4: TimeKeeper
     ```

3. **Role Quota**:
   - The number of nodes assigned to each role depends on network activity and transaction load.
   - During high transaction volumes, more nodes are assigned to critical roles (e.g., Validators).
   - Example for a network of 1,000 nodes:
     - **Proposers**: 10–15 nodes (1–1.5% of total nodes).
     - **Validators**: 300–400 nodes (30–40% of total nodes).
     - **Anchors**: 50–70 nodes (5–7% of total nodes).
     - **Cleaners**: 20–30 nodes (2–3% of total nodes).
     - **TimeKeepers**: 20–25 nodes (2–2.5% of total nodes).

---

### **2.3 Supporting and Backup Nodes**
1. **Supporting Functions**:
   - Nodes not actively assigned to critical roles during an interval contribute in auxiliary ways:
     - **Monitoring** network health and DAG consistency.
     - **Redundancy** for data storage and fault tolerance.
   - These tasks consume minimal resources, ensuring all nodes are utilized without unnecessary overhead.

2. **Backup Nodes**:
   - If active nodes become unresponsive or fail their role, backup nodes are immediately assigned to prevent interruptions.

3. **Dynamic Scaling**:
   - The number of active nodes scales dynamically based on network demand, ensuring efficiency during periods of low activity and robustness during high loads.

---

## **3. Role-Specific Assignment Details**

### **3.1 Proposer Assignment**
- **Criteria**:
  - Randomized selection ensures fairness.
  - Nodes with a history of high uptime are given slight priority.
- **Responsibilities**:
  - Bundle transactions into DAG Vertices.
  - Timestamp batches using Proof of History (PoH).
  - Broadcast vertices to Validators.

---

### **3.2 Validator Assignment**
- **Criteria**:
  - Validators must demonstrate:
    - Low latency.
    - Accurate validation in previous assignments.
- **Responsibilities**:
  - Verify DAG Vertices.
  - Check transaction authenticity and parent references.
  - Approve or reject vertices based on validation outcomes.

---

### **3.3 Anchor Assignment**
- **Criteria**:
  - Anchors are selected from nodes with consistent performance in previous roles.
- **Responsibilities**:
  - Finalize validated DAG Vertices.
  - Commit vertices to the ledger, ensuring immutability.

---

### **3.4 Cleaner Assignment**
- **Criteria**:
  - Randomized selection prioritizes nodes with available storage and bandwidth capacity.
- **Responsibilities**:
  - Identify and prune outdated DAG vertices.
  - Maintain an optimized and lightweight DAG structure.

---

### **3.5 TimeKeeper Assignment**
- **Criteria**:
  - Nodes with the lowest latency to the majority of their **Unique Node List (UNL)** are prioritized.
- **Responsibilities**:
  1. **Monitor Runtime Clocks**:
     - Ensure the local runtime clock aligns with the Governor Cryptographic Clock.
  2. **Measure Network Latency**:
     - Ping peers in the UNL and calculate the median latency buffer.
  3. **Synchronize Clocks**:
     - Adjust local clocks to maintain PoH consistency.
  4. **Identify Drift**:
     - Report nodes with significant clock drift for correction.

---

## **4. Advantages of Dynamic Role Assignment**

### 4.1 Fairness and Decentralization
- Dynamic assignment ensures all wallets contribute to the network.
- Randomization prevents centralization or dominance by specific wallets.

### 4.2 Scalability
- Roles dynamically scale with network activity, ensuring the system can handle increased transaction volumes.

### 4.3 Efficiency
- Role specialization reduces computational overhead, making the system accessible even on low-power devices.

### 4.4 Fault Tolerance
- Backup assignments and rebalancing mechanisms ensure network reliability, even if nodes fail to fulfill their roles.

---
