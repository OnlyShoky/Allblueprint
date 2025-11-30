# Data Quality and Governance

#data-quality #governance #data-catalog #data

> [!important] Trust Your Data
> Without data quality and governance, analytics and ML models produce garbage. "Garbage in, garbage out" isn't just a saying—it's reality.

**Related:** [[DataEngineering|Data Engineering]] · [[DataModeling|Data Modeling]] · [[MLOps|MLOps]] · [[../Cybersecurity/Data_Cloud_Security|Data Security]]

---

## Data Quality Dimensions

> [!success] Six Pillars of Quality
> Use these dimensions to assess and improve data quality systematically.

| Dimension | Question | Example Check |
|-----------|----------|---------------|
| **Accuracy** | Does it reflect reality? | Validate addresses against postal service |
| **Completeness** | Is any data missing? | Check for NULL values in required fields |
| **Consistency** | Same across systems? | Customer name matches in CRM and billing |
| **Timeliness** | Available when needed? | Data refreshed within SLA |
| **Uniqueness** | Any duplicates? | No duplicate user IDs |
| **Validity** | Follows format/rules? | Email matches regex, age > 0 |

**Related:** Foundation for [[MLOps#Model Monitoring|reliable ML models]].

---

## Data Quality Testing

### Great Expectations

**Concept:** Validate data before it enters warehouse or model.

```python
import great_expectations as ge

# Load data
df = ge.read_csv("data.csv")

# Define expectations
df.expect_column_values_to_be_unique("user_id")
df.expect_column_values_to_not_be_null("email")
df.expect_column_values_to_match_regex("email", r"^[\\w.-]+@[\\w.-]+\\.\\w+$")
df.expect_column_values_to_be_between("age", 0, 120)

# Validate
results = df.validate()
if not results.success:
    raise ValueError("Data quality check failed!")
```

> [!tip] Fail Fast
> Catch data quality issues in [[DataEngineering#Pipeline Orchestration|pipelines]] before bad data propagates downstream.

**Related:** Integrate into [[../BestPractices/CICD_DevOps|CI/CD for data]].

---

## Data Governance

**Definition:** Overall management of availability, usability, integrity, and security of data in an enterprise.

### Key Components

**Data Catalog:** Inventory of data assets with metadata.

**Tools:** Amundsen, DataHub, Alation

> [!success] Democratize Data Discovery
> Data catalogs enable self-service data discovery. No more asking "where is customer data?"

**Features:**
- Searchable metadata
- Column-level lineage
- Usage statistics
- Data ownership

---

### Data Lineage

**Concept:** Tracking data flow from origin to destination.

**Why it matters:**
- Impact analysis (what breaks if I change this table?)
- Compliance (GDPR data deletion requests)
- Debugging (where did this value come from?)
- Trust (can I rely on this metric?)

> [!important] End-to-End Visibility
> Lineage shows the complete journey of data through your systems, from source to dashboard.

**Tools:** Apache Atlas, DataHub, dbt (SQL lineage)

**Related:** Critical for [[../Cybersecurity/Data_Cloud_Security#Compliance|compliance]].

---

### Access Control

**Who can see what?**

**Patterns:**
- **Role-Based:** Data analysts can read, data engineers can write
- **Attribute-Based:** Sales team sees only their region's data
- **Dynamic Data Masking:** PII masked for non-privileged users

> [!warning] Data is a Liability
> More access = more risk. Implement least privilege for data access.

**Related:** Implements [[../Cybersecurity/Auth_Authorization#RBAC|RBAC principles]].

---

### Data Stewardship

**Concept:** Assigning owners to data domains.

**Responsibilities:**
- Define data quality rules
- Document data definitions
- Approve access requests
- Monitor data usage

> [!tip] Domain Ownership
> Data stewards are domain experts who understand the business context of data, not just technical aspects.

---

## Master Data Management (MDM)

**Problem:** Same entity (customer, product) has different IDs/attributes across systems.

**Solution:** Create golden record that reconciles conflicts.

**Example:** 
- System A: Customer "John Smith", email john@gmail.com
- System B: Customer "J. Smith", email j.smith@gmail.com
- MDM: Merge into single "John Smith" entity

---

## Data Governance Checklist

> [!success] Governance Essentials
> - [ ] Data catalog deployed and populated
> - [ ] Data owners assigned to all critical datasets
> - [ ] Data quality checks in every pipeline
> - [ ] Access controls properly configured
> - [ ] Data lineage tracked end-to-end
> - [ ] Sensitive data classified and protected
> - [ ] Documentation for all datasets
> - [ ] Regular data quality audits

---

## Further Reading

- Build quality into [[DataEngineering|pipelines]]
- Design schemas with [[DataModeling|good modeling]]
- Secure data via [[../Cybersecurity/Data_Cloud_Security|encryption and IAM]]
- Deploy reliable [[MLOps|ML models]]
- Test with [[../BestPractices/Testing_TDD_BDD|data validation]]

**Tags:** #data-quality #governance #data-catalog #lineage #stewardship
