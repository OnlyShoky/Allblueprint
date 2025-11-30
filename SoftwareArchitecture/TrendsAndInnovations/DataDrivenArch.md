# Data-Driven Architecture

**Definition:** An architectural approach where data is the primary asset and driver of the system design, rather than just a byproduct of processes.

## Key Concepts

### 1. Data Mesh
**Principle:** Decentralized data ownership.
**Shift:** From centralized Data Lake/Warehouse to domain-oriented data products.
**Pillars:**
- Domain-oriented ownership.
- Data as a product.
- Self-serve data infrastructure.
- Federated computational governance.

### 2. Data Fabric
**Principle:** An integrated layer of data and connecting processes.
**Goal:** Unified view of data across hybrid multi-cloud environments using metadata and AI/ML for automation.

### 3. Reverse ETL
**Concept:** Moving data *out* of the Data Warehouse and *into* operational tools (Salesforce, HubSpot, Production DBs).
**Why:** To operationalize analytics data (e.g., "High Churn Risk" flag pushed to CRM).

**Pros:**
- Better decision making.
- Democratization of data.
- Agility in data usage.

**Cons:**
- Cultural shift required.
- Complexity in governance.
