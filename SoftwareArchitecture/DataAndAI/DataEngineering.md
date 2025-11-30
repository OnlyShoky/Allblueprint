# Data Engineering

## Pipelines: ETL vs ELT

### ETL (Extract, Transform, Load)
**Process:** Data is extracted, transformed in a staging area, and then loaded into the destination (Warehouse).
**Use Case:** Legacy systems, when privacy requires masking before loading.

### ELT (Extract, Load, Transform)
**Process:** Data is loaded raw into the destination, then transformed using the destination's compute power (e.g., BigQuery, Snowflake).
**Use Case:** Modern Cloud Data Warehouses, Big Data.

## Storage Architectures

### Data Warehouse
**Structure:** Structured, schema-on-write.
**Purpose:** BI, Reporting, Analytics.
**Examples:** Snowflake, Redshift, BigQuery.

### Data Lake
**Structure:** Unstructured/Semi-structured, schema-on-read.
**Purpose:** ML, Data Science, Raw storage.
**Examples:** S3, ADLS, HDFS.

### Data Lakehouse
**Concept:** Combines best of both. ACID transactions on data lakes.
**Examples:** Databricks (Delta Lake), Apache Iceberg.

## Example Pipeline (Python/Airflow)
```python
from airflow import DAG
from airflow.operators.python import PythonOperator

def extract():
    # Pull data from API
    pass

def transform():
    # Clean data using Pandas
    pass

def load():
    # Upload to Snowflake
    pass

with DAG('etl_pipeline') as dag:
    e = PythonOperator(task_id='extract', python_callable=extract)
    t = PythonOperator(task_id='transform', python_callable=transform)
    l = PythonOperator(task_id='load', python_callable=load)
    
    e >> t >> l
```
