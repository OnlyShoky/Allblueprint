# Data Engineering

#data-engineering #etl #pipelines #data

> [!important] Foundation of Data Science
> Data engineering is the backbone of any data-driven organization. Without reliable data pipelines, machine learning and analytics cannot succeed.

**Related:** [[DataModeling|Data Modeling]] · [[MLOps|MLOps]] · [[DataQuality_Governance|Data Quality]] · [[../BestPractices/CICD_DevOps|CI/CD]]

---

## ETL vs ELT

### ETL (Extract, Transform, Load)

**Process:** Extract from source → Transform in staging → Load into destination (Data Warehouse).

**Use Case:** Legacy systems, when transformation must happen before loading (e.g., privacy masking).

> [!note] Traditional Approach
> ETL was the standard when compute was expensive and storage was cheap.

---

### ELT (Extract, Load, Transform)

**Process:** Extract from source → Load raw into destination → Transform using destination's compute power.

**Use Case:** Modern Cloud Data Warehouses (BigQuery, Snowflake, Redshift) with massive compute.

> [!success] Modern Approach
> ELT leverages cloud warehouse compute for transformations, enabling faster iteration and easier debugging.

**Related:** Enabled by [[../ModernArchitectures/CloudNative|cloud-native infrastructure]].

---

## Storage Architectures

### Data Warehouse

**Structure:** Structured, schema-on-write  
**Purpose:** BI, Reporting, Analytics  
**Examples:** Snowflake, Redshift, BigQuery

> [!tip] BI and Analytics
> Warehouses are optimized for complex analytical queries across large datasets.

---

### Data Lake

**Structure:** Unstructured/Semi-structured, schema-on-read  
**Purpose:** ML, Data Science, Raw storage  
**Examples:** S3, ADLS, HDFS

> [!note] Raw Data Storage
> Lakes store data in native format. Schema is applied when reading, enabling flexibility.

---

### Data Lakehouse

**Concept:** Combines best of both—ACID transactions on data lakes.  
**Examples:** Databricks (Delta Lake), Apache Iceberg, Apache Hudi

> [!success] Best of Both Worlds
> Lakehouse provides data lake flexibility with warehouse reliabil ity.

**Key Features:**
- ACID transactions
- Schema enforcement
- Time travel (versioning)
- Unified batch and streaming

**Related:** Used in [[MLOps|MLOps feature stores]].

---

## Pipeline Orchestration

### Apache Airflow

**Concept:** Workflow orchestration using Directed Acyclic Graphs (DAGs).

**Example Pipeline (Python):**
```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime

def extract():
    # Pull data from API
    print("Extracting...")

def transform():
    # Clean data using Pandas
    print("Transforming...")

def load():
    # Upload to Snowflake
    print("Loading...")

with DAG('etl_pipeline', start_date=datetime(2024, 1, 1), schedule='@daily') as dag:
    e = PythonOperator(task_id='extract', python_callable=extract)
    t = PythonOperator(task_id='transform', python_callable=transform)
    l = PythonOperator(task_id='load', python_callable=load)
    
    e >> t >> l  # Define dependencies
```

> [!tip] Infrastructure as Code
> DAGs are Python code, enabling version control, testing, and code review for data pipelines.

**Related:** Integrates with [[../BestPractices/CICD_DevOps|CI/CD pipelines]].

---

## Data Pipeline Patterns

### Batch Processing

**Frequency:** Hourly, daily, weekly  
**Tools:** Airflow, Luigi, dbt  
**Use Case:** Historical analysis, reporting

---

### Stream Processing

**Frequency:** Real-time, milliseconds  
**Tools:** Apache Kafka, Flink, Spark Streaming  
**Use Case:** Fraud detection, real-time dashboards

> [!important] Choose by Use Case
> Batch for historical analysis. Streaming for real-time decisions.

**Related:** Foundation of [[../ModernArchitectures/Serverless_EventDriven#Event-Driven|event-driven architecture]].

---

## Infrastructure

| Component | Purpose | Examples |
|-----------|---------|----------|
| **Storage** | Raw data | S3, GCS, ADLS |
| **Compute** | Processing | Spark, Dask, Presto |
| **Orchestration** | Workflow management | Airflow, Prefect, Dagster |
| **Transformation** | SQL transformations | dbt, Dataform |
| **Catalog** | Metadata discovery | Amundsen, DataHub |

**Related:** Deploy with [[../ModernArchitectures/CloudNative|cloud-native tools]].

---

## Further Reading

- Design schemas with [[DataModeling|data modeling]]
- Deploy models via [[MLOps|MLOps]]
- Ensure quality with [[DataQuality_Governance|data governance]]
- Automate with [[../BestPractices/CICD_DevOps|CI/CD]]
- Monitor with [[../BestPractices/Observability|observability]]

**Tags:** #data-engineering #etl #airflow #pipelines #data-warehouse
