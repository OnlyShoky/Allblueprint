# Data Quality and Governance

## Data Quality Dimensions
1. **Accuracy:** Does it reflect reality?
2. **Completeness:** Is any data missing?
3. **Consistency:** Is it the same across systems?
4. **Timeliness:** Is it available when needed?
5. **Uniqueness:** Are there duplicates?
6. **Validity:** Does it follow the format/rules?

## Data Governance
**Definition:** The overall management of the availability, usability, integrity, and security of data used in an enterprise.

### Key Components
- **Data Catalog:** Inventory of data assets (e.g., Amundsen, DataHub).
- **Data Lineage:** Tracking data flow from origin to destination.
- **Access Control:** Who can see what?
- **Stewardship:** Assigning owners to data domains.

## Testing Data (Great Expectations)
Validate data before it enters the warehouse or model.

```python
# Example concept
import great_expectations as ge

df = ge.read_csv("data.csv")
df.expect_column_values_to_be_unique("user_id")
df.expect_column_values_to_not_be_null("email")
```
