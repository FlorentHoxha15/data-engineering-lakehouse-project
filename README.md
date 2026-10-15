# 🏗️ End-to-End Data Engineering & Lakehouse Project

Welcome to my **Data Engineering & Lakehouse Project**! 🚀

This project demonstrates the development and evolution of an end-to-end Data Engineering solution using **SQL Server, Python, Pandas, PySpark, Apache Parquet, Databricks, Delta Lake, and Databricks Jobs**.

The project follows the **Medallion Architecture**, transforming data through **Bronze, Silver, and Gold layers**.

The repository intentionally keeps multiple implementations of the same Data Engineering problem to demonstrate the learning journey and evolution of the architecture:

- **Version 1:** Python + Pandas + SQL Server
- **Version 2:** PySpark + Apache Parquet
- **Version 3:** Databricks + PySpark + Delta Lake + Job Orchestration

This shows the progression from a traditional Python/SQL Data Warehouse pipeline toward a modern **Lakehouse architecture**.

---

# 📖 Project Overview

The goal of this project is to simulate a realistic Data Engineering workflow where data from multiple sources is collected, validated, transformed, stored, and prepared for analytics.

The project integrates:

- CRM data from CSV files
- ERP data from CSV files
- Historical currency exchange rates from a REST API

The project currently demonstrates:

- REST API ingestion
- CSV ingestion
- Raw JSON storage
- Data quality checks
- Incremental loading
- Watermark logic
- SQL Server
- Pandas
- PySpark
- Apache Spark
- Apache Parquet
- Partitioning
- Databricks
- Delta Lake
- Delta Tables
- Databricks Jobs
- Pipeline orchestration
- Medallion Architecture
- Bronze / Silver / Gold processing
- Data modeling
- Star Schema
- Analytics-ready datasets
- Logging and error handling
- Git / GitHub integration

---

# 🎯 Project Goal

The goal is to build an end-to-end Data Engineering project and continuously evolve it toward technologies and architectural patterns used in modern data platforms.

The project started with:

```text
Python + Pandas + SQL Server
```

It was then extended with:

```text
PySpark + Parquet + Partitioning
```

The latest implementation runs on:

```text
Databricks
    +
PySpark
    +
Delta Lake
    +
Medallion Architecture
    +
Databricks Jobs
```

The earlier implementations remain in the repository so that the complete technical progression is visible.

---

# 🛠️ Technologies Used

## Languages

- Python
- SQL
- T-SQL

## Data Processing

- Pandas
- PySpark
- Apache Spark

## Databases & Storage

- Microsoft SQL Server
- Apache Parquet
- Delta Lake
- Delta Tables

## Platform

- Databricks
- Databricks Notebooks
- Databricks Jobs & Pipelines
- Serverless Compute

## Data Sources

- REST APIs
- JSON
- CSV

## Python Libraries

- Requests
- SQLAlchemy
- PyODBC

## Data Engineering Concepts

- ETL / ELT
- Medallion Architecture
- Data Lakehouse
- Bronze / Silver / Gold
- Incremental Processing
- Watermark Logic
- Data Quality
- Partitioning
- Data Modeling
- Star Schema
- Pipeline Orchestration

## Development

- Git
- GitHub
- Databricks Git Folders
- Visual Studio Code

---

# 🏗️ Architecture

The project follows the **Medallion Architecture**:

```text
                 Source Systems
                       │
            ┌──────────┼──────────┐
            │          │          │
            ▼          ▼          ▼
           CRM        ERP      REST API
           CSV        CSV     Currency Data
            │          │          │
            └──────────┼──────────┘
                       │
                       ▼
                  🥉 BRONZE
                       │
                       ▼
                  🥈 SILVER
                       │
                       ▼
                   🥇 GOLD
                       │
                       ▼
              Analytics / Reporting
```

Each layer has a different responsibility.

### 🥉 Bronze

Stores ingested data with minimal transformation.

### 🥈 Silver

Contains cleaned, validated, standardized, and deduplicated data.

### 🥇 Gold

Contains business-ready and aggregated datasets for analytics and reporting.

---

# 📥 Data Sources

## CRM

CSV files containing:

- Customer data
- Product data
- Sales data

## ERP

CSV files containing:

- Customer information
- Location information
- Product category information

## Currency REST API

Historical EUR exchange rates are retrieved from the **Frankfurter REST API**.

Currencies:

- USD
- GBP
- CHF

The currency data covers the sales period:

```text
2010-12-29 → 2014-01-28
```

---

# 🐍 Version 1 — Pandas + SQL Server

The first implementation uses:

```text
Python
   +
Pandas
   +
SQLAlchemy
   +
SQL Server
```

## Pipeline Flow

```text
Frankfurter REST API
        │
        ▼
Python Requests
        │
        ▼
Raw JSON
        │
        ▼
Pandas DataFrame
        │
        ▼
Data Preparation
        │
        ▼
Data Quality Checks
        │
        ▼
Watermark Check
        │
        ▼
Incremental Loading
        │
        ▼
🥉 SQL Server Bronze
        │
        ▼
🥈 SQL Server Silver
        │
        ▼
🥇 SQL Server Gold
        │
        ▼
Analytics
```

## Features

The original pipeline demonstrates:

- REST API extraction
- Raw JSON storage
- Pandas DataFrames
- Date conversion
- NULL checks
- Duplicate checks
- Data type validation
- Invalid exchange-rate detection
- SQLAlchemy database connectivity
- SQL Server integration
- Watermark logic
- Incremental loading
- Stored procedures
- Logging
- Error handling

---

# ⚡ Version 2 — PySpark + Parquet

The second implementation rebuilds the currency pipeline using **PySpark**.

Instead of processing the data primarily with Pandas and storing each layer in SQL Server, this implementation uses:

- Spark DataFrames
- Spark transformations
- Apache Parquet
- Partitioning
- Spark-based watermark logic
- Incremental processing

## Pipeline Flow

```text
Frankfurter REST API
        │
        ▼
Raw JSON
        │
        ▼
PySpark DataFrame
        │
        ▼
Data Preparation
        │
        ▼
Data Quality Checks
        │
        ▼
Watermark Check
        │
        ▼
Incremental Processing
        │
        ▼
🥉 Bronze Parquet
        │
        ▼
PySpark Transformations
        │
        ▼
🥈 Silver Parquet
        │
        ▼
PySpark Aggregations
        │
        ▼
🥇 Gold Parquet
        │
        ▼
Analytics / Reporting
```

---

# ⚡ PySpark Processing

The PySpark pipeline uses a `SparkSession` to process data using Spark DataFrames.

The pipeline performs:

- Spark DataFrame creation
- Date conversion with `to_date()`
- Numeric conversion with `cast()`
- NULL handling
- Duplicate removal
- Filtering
- Data quality validation
- Aggregations
- Incremental processing
- Parquet reads and writes
- Partitioning

Example:

```python
df = df.withColumn(
    "rate",
    col("rate").cast("double")
)
```

---

# 🔍 Data Quality

Data quality validation is performed before data continues through the pipeline.

```text
Incoming Data
      │
      ▼
Convert Data Types
      │
      ▼
Remove NULLs
      │
      ▼
Remove Duplicates
      │
      ▼
Check Invalid Rates
      │
      ▼
Continue Pipeline
```

An exchange rate is considered invalid when:

```text
rate <= 0
```

If invalid rates are detected, the affected data does not continue through the pipeline.

---

# 🔄 Watermark & Incremental Processing

The currency pipeline uses a **watermark** to avoid repeatedly loading the same API records.

The watermark represents:

> The latest date that has already been processed.

Conceptually:

```text
API Data
   │
   ▼
Bronze
   │
   ▼
MAX(date)
   │
   ▼
Watermark
   │
   ▼
date > watermark
   │
   ▼
Only New Records
```

If Bronze does not exist yet:

```text
watermark = None
```

This represents the first pipeline run, so all available API records can be processed.

---

# 🥉 Bronze Layer — PySpark

The standalone PySpark implementation stores incrementally ingested currency data in Parquet.

Only records newer than the watermark are appended.

```python
new_data.write \
    .mode("append") \
    .partitionBy("quote") \
    .parquet(BRONZE_PATH)
```

The data is partitioned by currency:

```text
bronze/currency_rates/

├── quote=USD/
├── quote=GBP/
└── quote=CHF/
```

Partitioning organizes the dataset by currency and can reduce unnecessary data scanning when Spark filters on the partition column.

---

# 🥈 Silver Layer — PySpark

After new records are added to Bronze, the standalone PySpark pipeline reads the complete Bronze dataset.

```text
Bronze
   │
   ▼
Read Complete Dataset
   │
   ▼
Remove Duplicates
   │
   ▼
Validate Rates
   │
   ▼
Silver
```

Silver contains cleaned and validated currency data.

The transformation includes:

- Duplicate removal
- Invalid-rate filtering
- Clean data types
- Valid currency records

Silver is also stored as partitioned Parquet.

```text
silver/currency_rates/

├── quote=USD/
├── quote=GBP/
└── quote=CHF/
```

---

# 🥇 Gold Layer — PySpark

The Gold layer transforms the cleaned Silver data into a simple analytical currency summary.

The data is grouped by:

```text
quote
```

The pipeline calculates:

- Average exchange rate
- Minimum exchange rate
- Maximum exchange rate

Example:

```text
quote | average_rate | min_rate | max_rate
------------------------------------------------
USD   | 1.35         | 1.20     | 1.48
GBP   | 0.84         | 0.78     | 0.91
CHF   | 1.18         | 1.02     | 1.32
```

The transformation uses PySpark aggregations:

```python
gold_df = silver_df.groupBy(
    "quote"
).agg(
    avg("rate").alias("average_rate"),
    min("rate").alias("min_rate"),
    max("rate").alias("max_rate")
)
```

---

# 📦 Why Parquet?

The standalone PySpark implementation uses **Apache Parquet** for its Medallion layers.

Parquet provides:

- Column-oriented storage
- Compression
- Data type preservation
- Efficient analytical reads
- Strong Spark integration
- Partitioning support

This makes Parquet well suited for analytical Data Engineering workloads.

---

# 📂 Partitioning

The standalone PySpark Bronze and Silver datasets are partitioned by:

```text
quote
```

Example:

```text
currency_rates/

├── quote=USD/
├── quote=GBP/
└── quote=CHF/
```

When Spark filters on a partition column, partition pruning can reduce unnecessary data scanning.

Example:

```python
df.filter(
    col("quote") == "USD"
)
```

The Gold currency summary is very small and therefore does not require partitioning.

---

# 🧱 Version 3 — Databricks Lakehouse

The latest version moves the currency pipeline into **Databricks**.

This implementation uses:

- Databricks Notebooks
- PySpark
- Delta Lake
- Delta Tables
- Medallion Architecture
- Watermark-based incremental ingestion
- Data quality validation
- Databricks Jobs
- Task dependencies
- GitHub integration

The architecture is now:

```text
Frankfurter REST API
        │
        ▼
Databricks
        │
        ▼
PySpark DataFrame
        │
        ▼
Watermark
        │
        ▼
Incremental Filter
        │
        ▼
🥉 Bronze Delta Table
        │
        ▼
Cleaning & Data Quality
        │
        ▼
🥈 Silver Delta Table
        │
        ▼
PySpark Aggregations
        │
        ▼
🥇 Gold Delta Table
        │
        ▼
Analytics
```

---

# 🥉 Databricks Bronze Layer

The Databricks Bronze notebook is responsible for ingesting currency data from the REST API.

Notebook:

```text
databricks/bronze/bronze_currency.ipynb
```

The notebook performs:

```text
Frankfurter API
      ↓
JSON Response
      ↓
Spark DataFrame
      ↓
Watermark
      ↓
Incremental Filter
      ↓
Bronze Delta Table
```

The watermark is retrieved from the existing Bronze table:

```sql
SELECT MAX(date) AS watermark
FROM bronze.currency_rates
```

Only records newer than the watermark continue:

```python
def filter_new_data(df, watermark):
    if watermark is None:
        new_data = df
    else:
        new_data = df.filter(
            col("date") > watermark
        )

    return new_data
```

The new records are written to:

```text
bronze.currency_rates
```

using Delta format:

```python
new_data.write \
    .format("delta") \
    .mode("append") \
    .saveAsTable("bronze.currency_rates")
```

---

# 🥈 Databricks Silver Layer

Notebook:

```text
databricks/silver/silver_currency.ipynb
```

Silver reads the Bronze Delta Table:

```python
df = spark.table("bronze.currency_rates")
```

The data is then cleaned and standardized.

Transformations include:

- Convert `date` to a date type
- Convert `rate` to double
- Trim currency values
- Standardize currency codes to uppercase
- Remove duplicate records
- Validate NULL values
- Validate exchange rates

The data quality check verifies that:

```text
date  != NULL
base  != NULL
quote != NULL
rate  != NULL
rate  > 0
```

Valid data is written to:

```text
silver.currency_rates
```

as a Delta Table.

---

# 🥇 Databricks Gold Layer

Notebook:

```text
databricks/gold/gold_currency.ipynb
```

Gold reads:

```text
silver.currency_rates
```

and creates an analytics-ready currency summary.

The data is grouped by currency and calculates:

```text
AVG(rate)
MIN(rate)
MAX(rate)
```

The final Delta Table is:

```text
gold.currency_summary
```

Example structure:

```text
quote | average_rate | min_rate | max_rate
------------------------------------------------
USD   | ...          | ...      | ...
GBP   | ...          | ...      | ...
CHF   | ...          | ...      | ...
```

---

# 🔺 Why Delta Lake?

The Databricks implementation uses **Delta Tables** instead of plain Parquet datasets.

Conceptually:

```text
Delta Table
     =
Parquet Data
     +
Transaction Log
```

Delta Lake adds functionality such as:

- ACID transactions
- Reliable writes
- UPDATE
- DELETE
- MERGE
- Table versioning
- Schema management
- Transaction history

This makes Delta Tables better suited for managed Lakehouse pipelines than plain Parquet files alone.

---

# 🔄 Databricks Job Orchestration

The three Databricks notebooks are orchestrated using a **Databricks Job**.

Job:

```text
Currency Lakehouse Pipeline
```

Task dependency flow:

```text
bronze_currency
       │
       ▼
silver_currency
       │
       ▼
gold_currency
```

The dependencies ensure that:

```text
Bronze succeeds
      ↓
Silver starts

Silver succeeds
      ↓
Gold starts
```

If an upstream task fails, downstream processing does not continue.

The complete Job successfully executes the currency pipeline from API ingestion to the Gold analytics table.

---

# ⚙️ Automated Pipeline Flow

The Databricks implementation combines ingestion, transformation and orchestration:

```text
                 Databricks Job
                       │
                       ▼
               bronze_currency
                       │
                       ▼
             Frankfurter REST API
                       │
                       ▼
                Watermark Check
                       │
                       ▼
               Incremental Data
                       │
                       ▼
            bronze.currency_rates
                       │
                       ▼
               silver_currency
                       │
                       ▼
             Cleaning + Validation
                       │
                       ▼
            silver.currency_rates
                       │
                       ▼
                gold_currency
                       │
                       ▼
                 Aggregation
                       │
                       ▼
            gold.currency_summary
```

This removes the need to manually execute each notebook separately.

---

# 🏠 Data Warehouse vs Lakehouse

This repository demonstrates two architectural approaches.

## Traditional Data Warehouse

The original implementation uses:

```text
Python
  ↓
Pandas
  ↓
SQL Server
  ↓
Bronze / Silver / Gold
```

## Data Lakehouse

The latest implementation uses:

```text
Databricks
  ↓
PySpark
  ↓
Delta Lake
  ↓
Bronze / Silver / Gold
  ↓
Databricks Jobs
```

The Lakehouse implementation combines scalable file-based data processing with managed tables and Data Warehouse-style capabilities.

---

# 🧠 Pipeline Evolution

One of the main goals of this repository is to show how the project evolved while learning Data Engineering.

## Version 1

```text
REST API
   ↓
Python
   ↓
Pandas
   ↓
SQLAlchemy
   ↓
SQL Server Bronze
   ↓
SQL Server Silver
   ↓
SQL Server Gold
```

## Version 2

```text
REST API
   ↓
Python
   ↓
PySpark
   ↓
Incremental Processing
   ↓
Bronze Parquet
   ↓
Silver Parquet
   ↓
Gold Parquet
```

## Version 3

```text
REST API
   ↓
Databricks
   ↓
PySpark
   ↓
Watermark
   ↓
Bronze Delta
   ↓
Silver Delta
   ↓
Gold Delta
   ↓
Databricks Job
```

The earlier implementations are intentionally preserved.

The objective is not to show that one technology is always better than another. Instead, the repository demonstrates how the same Data Engineering problem can evolve as new technologies and architectural concepts are introduced.

---

# 💱 SQL Currency Integration

The original SQL Server implementation integrates historical exchange rates with sales data.

Sales data is connected to currency data using:

```text
fact_sales.order_date
        │
        ▼
api_currency_rates.date
```

Example:

```text
Sales Amount
€3,578

Historical EUR → USD Rate
1.3155

Converted Sales
€3,578 × 1.3155 = $4,706.86
```

The resulting analytical SQL view is:

```text
gold.fact_sales_currency
```

It contains:

- Order Number
- Product Key
- Customer Key
- Order Date
- EUR Sales Amount
- Target Currency
- Historical Exchange Rate
- Converted Sales Amount

---

# ⭐ SQL Server Data Model

The original SQL Server implementation also contains a Star Schema.

```text
             dim_customers
                   │
                   ▼
dim_products ──► fact_sales
```

Gold objects include:

```text
gold.dim_customers
gold.dim_products
gold.fact_sales
gold.fact_sales_currency
```

This allows the project to demonstrate both:

- Data pipeline engineering
- Analytical data modeling

---

# ⚠️ Project Assumption

The original sales dataset does not contain a currency field.

For demonstration purposes, the original `sales_amount` values are treated as **EUR**.

Historical EUR exchange rates are retrieved from the currency API and used to calculate equivalent values in:

- USD
- GBP
- CHF

This assumption allows the project to demonstrate API ingestion, historical currency conversion, and multi-source data integration.

---

# 🧩 Modular Pipeline Design

The standalone PySpark pipeline is divided into reusable functions.

```text
create_spark_session()

extract_currency_data()
save_raw_data()

create_dataframe()

convert_date_column()
convert_rate_column()
remove_nulls()
remove_duplicates()

check_invalid_rates()
check_data_quality()

get_watermark()
filter_new_data()
check_new_data()

load_bronze()
read_bronze()

transform_silver()
load_silver()
read_silver()

transform_gold()
load_gold()

main()
```

The `main()` function coordinates the complete standalone PySpark pipeline.

```text
Extract
   ↓
Prepare
   ↓
Validate
   ↓
Watermark
   ↓
Incremental Processing
   ↓
Bronze
   ↓
Silver
   ↓
Gold
```

In Databricks, these responsibilities are separated into Bronze, Silver and Gold notebooks and orchestrated through a Databricks Job.

---

# 📝 Logging & Error Handling

The standalone Python/PySpark pipeline logs important execution events.

Examples include:

- Pipeline started
- API extraction successful
- Number of extracted records
- Raw JSON saved
- Current watermark
- Number of new records
- Bronze load successful
- Silver load successful
- Gold load successful
- Pipeline completed
- Pipeline failed

The pipeline handles API-specific exceptions:

```python
except requests.RequestException as error:
```

and unexpected errors:

```python
except Exception as error:
```

This prevents failures from happening silently and makes troubleshooting easier.

---

# 📂 Repository Structure

```text
sql-data-warehouse-project/
│
├── databricks/
│   │
│   ├── bronze/
│   │   └── bronze_currency.ipynb
│   │
│   ├── silver/
│   │   └── silver_currency.ipynb
│   │
│   └── gold/
│       └── gold_currency.ipynb
│
├── datasets/
│   ├── source_crm/
│   ├── source_erp/
│   └── source_api/
│       └── currency_raw.json
│
├── python/
│   └── ingestion/
│       ├── load_data.py
│       └── currency_pipeline_pyspark.py
│
├── scripts/
│   ├── bronze/
│   │   ├── ddl_bronze.sql
│   │   └── proc_load_bronze.sql
│   │
│   ├── silver/
│   │   ├── ddl_silver.sql
│   │   └── proc_load_silver.sql
│   │
│   └── gold/
│       └── ddl_gold.sql
│
├── LICENSE
└── README.md
```

---

# 📓 Databricks Notebooks

## `bronze_currency.ipynb`

Responsible for:

- REST API extraction
- Spark DataFrame creation
- Watermark retrieval
- Incremental filtering
- Bronze Delta ingestion

Output:

```text
bronze.currency_rates
```

## `silver_currency.ipynb`

Responsible for:

- Reading Bronze
- Data type conversion
- Standardization
- Duplicate removal
- Data quality validation
- Silver Delta loading

Output:

```text
silver.currency_rates
```

## `gold_currency.ipynb`

Responsible for:

- Reading Silver
- Grouping by currency
- Average-rate calculation
- Minimum-rate calculation
- Maximum-rate calculation
- Gold Delta loading

Output:

```text
gold.currency_summary
```

---

# 🐍 Python Pipelines

## `load_data.py`

Original implementation using:

```text
Python
Pandas
SQLAlchemy
SQL Server
```

It demonstrates:

- API extraction
- Pandas processing
- Data quality
- SQL Server connectivity
- Watermark logic
- Incremental loading
- Stored procedure execution

## `currency_pipeline_pyspark.py`

Standalone Spark implementation using:

```text
Python
PySpark
Apache Spark
Parquet
```

It demonstrates:

- SparkSession
- Spark DataFrames
- Data cleaning
- Data quality
- Watermark logic
- Incremental processing
- Parquet
- Partitioning
- Bronze processing
- Silver transformations
- Gold aggregations

---

# 📊 Analytics

The project supports analysis such as:

## Customer Analysis

- Customer purchasing patterns
- Customer contribution to revenue

## Product Analysis

- Best-performing products
- Product categories
- Product sales performance

## Sales Analysis

- Revenue trends
- Sales over time
- Business performance

## Currency Analysis

- Historical exchange rates
- Average exchange rate by currency
- Minimum exchange rate
- Maximum exchange rate
- EUR → USD conversion
- EUR → GBP conversion
- EUR → CHF conversion

---

# 🧠 Skills Demonstrated

## SQL

- T-SQL
- SQL Server
- Stored Procedures
- Window Functions
- Joins
- Data Cleaning
- Data Transformation
- Fact Tables
- Dimension Tables
- Star Schema
- Medallion Architecture

## Python

- Python
- Pandas
- REST APIs
- Requests
- JSON
- SQLAlchemy
- PyODBC
- Functions
- Exception Handling
- Logging
- Modular Pipeline Development

## PySpark

- Apache Spark
- SparkSession
- Spark DataFrames
- `select()`
- `filter()`
- `withColumn()`
- `cast()`
- `to_date()`
- `dropna()`
- `dropDuplicates()`
- `groupBy()`
- `agg()`
- Spark aggregations
- Parquet reads and writes
- Partitioning
- Partition pruning concepts

## Databricks

- Databricks Notebooks
- Serverless Compute
- Delta Tables
- Bronze / Silver / Gold
- Databricks Jobs
- Task Dependencies
- Job Runs
- Pipeline Orchestration
- GitHub Integration
- Databricks Git Folders

## Data Engineering

- ETL / ELT
- Data Ingestion
- REST API Ingestion
- Data Quality
- Incremental Processing
- Watermark Logic
- Medallion Architecture
- Data Lakehouse
- Bronze / Silver / Gold
- Parquet
- Delta Lake
- Partitioning
- Multi-source Data Integration
- Data Modeling
- Pipeline Orchestration
- Logging
- Error Handling
- Git
- GitHub

---

# 🚀 Key Learning Outcomes

Through this project, I learned how to build and gradually evolve an end-to-end Data Engineering pipeline.

The project demonstrates how to:

1. Ingest data from CSV files and REST APIs.
2. Preserve raw API data as JSON.
3. Process data using Pandas.
4. Process data using PySpark.
5. Create and transform Spark DataFrames.
6. Validate data quality.
7. Handle NULL values and duplicates.
8. Convert data types.
9. Implement watermark logic.
10. Process only new records.
11. Build incremental pipelines.
12. Store analytical datasets using Parquet.
13. Partition datasets.
14. Understand partition pruning.
15. Build Bronze, Silver, and Gold layers.
16. Perform Spark aggregations.
17. Build SQL Server fact and dimension models.
18. Integrate historical currency data with sales data.
19. Add logging and error handling.
20. Structure pipelines into reusable functions.
21. Build Delta Tables in Databricks.
22. Build a Data Lakehouse architecture.
23. Separate processing into Databricks notebooks.
24. Configure task dependencies.
25. Orchestrate Bronze → Silver → Gold using Databricks Jobs.
26. Connect Databricks with GitHub.
27. Evolve the same project across multiple Data Engineering technologies.

---

# 🔄 Current Project Status

The project has now progressed through:

```text
SQL Server
     │
     ▼
Python + Pandas
     │
     ▼
REST API Pipeline
     │
     ▼
Watermark & Incremental Loading
     │
     ▼
PySpark
     │
     ▼
Parquet & Partitioning
     │
     ▼
Bronze / Silver / Gold
     │
     ▼
Databricks
     │
     ▼
Delta Lake
     │
     ▼
Data Lakehouse
     │
     ▼
Databricks Job Orchestration
```

The currency API pipeline is now implemented as an end-to-end Databricks Lakehouse pipeline.

---

# 🔜 Next Steps

The next phase of the project will expand the Databricks implementation beyond the currency API.

The existing CRM and ERP CSV datasets will also be migrated into the Databricks Lakehouse.

Planned architecture:

```text
                 Source Systems
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
       CRM CSV      ERP CSV      REST API
          │            │            │
          └────────────┼────────────┘
                       │
                       ▼
                 Databricks
                       │
                       ▼
                  🥉 Bronze
                       │
                       ▼
                  🥈 Silver
                       │
                       ▼
                   🥇 Gold
                       │
                       ▼
                Star Schema
                       │
                       ▼
              Analytics / Reporting
```

Future improvements include:

- Ingest CRM CSV files into Databricks
- Ingest ERP CSV files into Databricks
- Build Bronze Delta Tables for all source systems
- Build Silver transformations for CRM and ERP
- Integrate API, CRM and ERP data
- Build Gold fact and dimension tables
- Build a Databricks Star Schema
- Expand Databricks Job orchestration
- Add scheduling
- Add pipeline monitoring
- Explore cloud storage integration

The objective is to continue evolving the same project while preserving earlier implementations to demonstrate the complete Data Engineering learning journey.

---

# 🛡️ License

This project is licensed under the **MIT License**.

See the `LICENSE` file for more information.
