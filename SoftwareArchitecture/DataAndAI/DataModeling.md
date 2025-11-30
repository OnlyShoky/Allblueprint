# Data Modeling

## Relational Modeling (SQL)

### Normalization (3NF)
**Goal:** Reduce redundancy and improve integrity.
**Rules:**
1. Atomic values.
2. No partial dependencies.
3. No transitive dependencies.

### Dimensional Modeling (Star Schema)
**Context:** Data Warehousing.
**Components:**
- **Fact Table:** Measurements/Metrics (Sales, Clicks).
- **Dimension Table:** Context (Time, Product, Customer).

**Diagram:**
```
       [Time Dim]
           |
[Product]--[Sales Fact]--[Customer]
           |
       [Store Dim]
```

## NoSQL Modeling

### Document (MongoDB)
**Pattern:** Embedding vs Referencing.
- **Embedding:** Read performance (one seek).
- **Referencing:** Data consistency, many-to-many.

### Key-Value (Redis, DynamoDB)
**Pattern:** Access patterns drive design.
- **Composite Keys:** Partition Key + Sort Key.
- **GSI (Global Secondary Index):** For alternative query patterns.

### Graph (Neo4j)
**Pattern:** Nodes and Relationships.
**Use Case:** Social networks, Recommendation engines, Fraud detection.
