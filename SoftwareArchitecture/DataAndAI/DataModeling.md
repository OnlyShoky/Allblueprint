# Data Modeling

#data-modeling #database #schema-design #sql #nosql

> [!important] Schema Design Matters
> Good data modeling is the foundation of performant, maintainable systems. Poor schemas lead to complex queries, slow performance, and data quality issues.

**Related:** [[DataEngineering|Data Engineering]] · [[DataQuality_Governance|Data Governance]] · [[../Best Practices/Scalability_Resilience|Scalability]]

---

## Relational Modeling (SQL)

### Normalization (3NF)

**Goal:** Reduce redundancy and improve data integrity.

**Normalization Levels:**

| Form | Rule |
|------|------|
| **1NF** | Atomic values (no arrays or nested structures) |
| **2NF** | No partial dependencies (all non-key attributes depend on entire primary key) |
| **3NF** | No transitive dependencies (non-key attributes depend only on primary key) |

> [!tip] Balance Normalization
> High normalization = data integrity. De-normalization = read performance. Balance based on use case.

**Related:** Essential for [[DataQuality_Governance#Data Quality|data quality]].

---

### Dimensional Modeling (Star Schema)

**Context:** Data Warehousing for analytics.

**Components:**
- **Fact Table:** Measurements/Metrics (Sales amount, Click counts, Revenue)
- **Dimension Table:** Context (Time, Product, Customer, Location)

**Diagram:**
```
       [Time Dim]
           |
[Product]--[Sales Fact]--[Customer]
           |
       [Store Dim]
```

> [!success] Optimized for Analytics
> Star schema enables fast, intuitive queries for business intelligence and reporting.

**Example Schema:**
```sql
-- Fact Table
CREATE TABLE sales_fact (
    sale_id BIGINT PRIMARY KEY,
    product_id INT REFERENCES product_dim(product_id),
    customer_id INT REFERENCES customer_dim(customer_id),
    date_id INT REFERENCES time_dim(date_id),
    amount DECIMAL(10,2),
    quantity INT
);

-- Dimension Table
CREATE TABLE product_dim (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(255),
    category VARCHAR(100),
    brand VARCHAR(100)
);
```

**Related:** Used in [[DataEngineering#Data Warehouse|data warehouses]].

---

## NoSQL Modeling

> [!note] Access Patterns Drive Design
> Unlike SQL, NoSQL modeling starts with "What queries will I run?" Design the schema to optimize those access patterns.

### Document (MongoDB)

**Pattern:** Embedding vs Referencing.

**Embedding (Denormalization):**
```json
{
  "_id": "order123",
  "customer": {
    "name": "John Doe",
    "email": "john@example.com"
  },
  "items": [
    {"product": "Laptop", "price": 1200},
    {"product": "Mouse", "price": 25}
  ]
}
```

**Pros:** One query, fast reads  
**Cons:** Data duplication

**Referencing (Normalization):**
```json
{
  "_id": "order123",
  "customer_id": "cust456",
  "item_ids": ["item789", "item012"]
}
```

**Pros:** No duplication, easier updates  
**Cons:** Multiple queries (joins)

---

### Key-Value (Redis, DynamoDB)

**Pattern:** Composite keys and access patterns.

**DynamoDB Example:**
- **Partition Key:** `user_id`
- **Sort Key:** `timestamp`
- **GSI (Global Secondary Index):** Query by `email`

> [!tip] Design for Your Queries
> DynamoDB requires you to know your access patterns upfront. You cannot efficiently run arbitrary queries.

**Related:** Critical for [[../BestPractices/Scalability_Resilience#Scalability|high-scale applications]].

---

### Graph (Neo4j)

**Pattern:** Nodes and Relationships.

**Use Case:** Social networks, recommendation engines, fraud detection, knowledge graphs.

**Example (Cypher Query):**
```cypher
// Find friends of friends
MATCH (user:Person {name: 'Alice'})-[:FRIENDS_WITH]->(friend)-[:FRIENDS_WITH]->(fof)
WHERE NOT (user)-[:FRIENDS_WITH]->(fof) AND user <> fof
RETURN fof.name
```

> [!success] Perfect for Connections
> Graph databases excel at querying relationships and traversing connections.

---

## Modeling Anti-Patterns

| Anti-Pattern | Description | Better Approach |
|--------------|-------------|-----------------|
| **God Table** | One massive table with everything | Normalize into logical entities |
| **EAV (Entity-Attribute-Value)** | Flexible but slow | Use JSON columns or proper schema |
| **UUID as Primary Key** | Poor performance for indexes | Use auto-incrementing integers or UUIDs wisely |
| **Premature Optimization** | Over-indexing everything | Index based on actual query patterns |

---

## Further Reading

- Build pipelines with [[DataEngineering|data engineering]]
- Ensure quality via [[DataQuality_Governance|governance]]
- Deploy ML with [[MLOps|feature stores]]
- Scale with [[../BestPractices/Scalability_Resilience|scalability patterns]]

**Tags:** #data-modeling #database #sql #nosql #star-schema #normalization
