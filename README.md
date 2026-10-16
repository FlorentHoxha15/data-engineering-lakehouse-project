# 🏗️ End-to-End Data Engineering & Lakehouse Project

Welcome to my **End-to-End Data Engineering & Lakehouse Project**! 🚀

This project demonstrates the development and evolution of a complete Data Engineering solution using:

**SQL Server · Python · Pandas · PySpark · Apache Spark · Parquet · Databricks · Delta Lake · Databricks Jobs**

The project follows the **Medallion Architecture** and processes data through **Bronze, Silver, and Gold layers**.

The repository intentionally preserves multiple implementations of the same Data Engineering problem to demonstrate the progression from a traditional Data Warehouse pipeline toward a modern **Databricks Lakehouse architecture**.

### Project Evolution

**Version 1 — Python + Pandas + SQL Server**

**Version 2 — PySpark + Apache Parquet**

**Version 3 — Databricks + PySpark + Delta Lake + Job Orchestration**

---

# 📖 Project Overview

The goal of this project is to simulate a realistic end-to-end Data Engineering workflow where data from multiple source systems is ingested, cleaned, validated, transformed, modeled, and prepared for analytics.

The project integrates three main data sources:

- CRM CSV files
- ERP CSV files
- Historical currency exchange rates from a REST API

The latest Databricks implementation processes all three sources through a Lakehouse architecture.

```text
                 Source Systems
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
       CRM CSV      ERP CSV      REST API
          │            │         Currency
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

---

# 🎯 Project Goals

This project was built to practice and demonstrate core Data Engineering concepts in a realistic architecture.

It includes:

- Multi-source data ingestion
- CSV ingestion
- REST API ingestion
- Raw JSON storage
- Data cleaning and transformation
- Data quality validation
- Incremental loading
- Watermark logic
- PySpark processing
- Apache Parquet
- Partitioning
- Delta Lake
- Delta Tables
- Medallion Architecture
- Dimensional modeling
- Star Schema
- Fact and dimension tables
- Historical currency conversion
- Databricks Jobs
- Task dependencies
- Pipeline orchestration
- Git / GitHub integration

---

# 🛠️ Technology Stack

## Languages

- Python
- SQL
- T-SQL

## Data Processing

- Pandas
- PySpark
- Apache Spark

## Database & Storage

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

- CSV
- JSON
- REST API

## Python Libraries

- Requests
- Pandas
- SQLAlchemy
- PyODBC
- PySpark

## Development

- Git
- GitHub
- Databricks Git Folders
- Visual Studio Code

---

# 🏗️ Medallion Architecture

The project follows the **Bronze → Silver → Gold** Medallion Architecture.

## 🥉 Bronze Layer

The Bronze layer stores ingested source data with minimal transformation.

Sources include:

- CRM customer data
- CRM product data
- CRM sales data
- ERP customer data
- ERP location data
- ERP product categories
- Currency exchange rates from the Frankfurter REST API

## 🥈 Silver Layer

The Silver layer cleans, validates, standardizes, and deduplicates the Bronze data.

Transformations include:

- Data type conversion
- NULL handling
- Duplicate removal
- Date conversion
- Text trimming
- Country standardization
- Gender standardization
- Marital-status standardization
- Product-line standardization
- Invalid sales correction
- Product validity periods
- Exchange-rate validation

## 🥇 Gold Layer

The Gold layer contains business-ready analytical datasets.

The CRM/ERP Gold layer follows a **Star Schema** containing:

```text
gold.dim_customers
gold.dim_products
gold.fact_sales
gold.fact_sales_currency
```

The currency pipeline additionally creates:

```text
gold.currency_summary
```

---

# 📥 Data Sources

## CRM Data

The CRM source contains three CSV datasets:

```text
cust_info.csv
prd_info.csv
sales_details.csv
```

These contain:

- Customer information
- Product information
- Sales transactions

## ERP Data

The ERP source contains:

```text
CUST_AZ12.csv
LOC_A101.csv
PX_CAT_G1V2.csv
```

These provide:

- Additional customer information
- Customer locations
- Product categories

## Currency REST API

Historical exchange rates are retrieved from the **Frankfurter REST API**.

The project processes EUR exchange rates for:

- USD
- GBP
- CHF

The currency dataset covers the sales period:

```text
2010-12-29 → 2014-01-28
```

---

# 🐍 Version 1 — Python + Pandas + SQL Server

The first version of the project uses a traditional Data Engineering architecture.

```text
REST API / CSV
      │
      ▼
    Python
      │
      ▼
    Pandas
      │
      ▼
Data Quality
      │
      ▼
Watermark Logic
      │
      ▼
  SQL Server
      │
      ▼
🥉 Bronze
      │
      ▼
🥈 Silver
      │
      ▼
🥇 Gold
```

This version demonstrates:

- Python data ingestion
- REST API extraction
- Pandas transformations
- Raw JSON storage
- SQLAlchemy connectivity
- SQL Server
- Stored procedures
- Watermark logic
- Incremental loading
- Data quality validation
- Logging
- Error handling
- Dimensional modeling

The SQL Server implementation contains the following Gold objects:

```text
gold.dim_customers
gold.dim_products
gold.fact_sales
gold.fact_sales_currency
```

---

# ⚡ Version 2 — PySpark + Apache Parquet

The second version rebuilds the currency pipeline using **PySpark**.

Instead of primarily processing data with Pandas, this version uses distributed Spark transformations.

```text
REST API
   │
   ▼
Raw JSON
   │
   ▼
PySpark DataFrame
   │
   ▼
Data Quality
   │
   ▼
Watermark
   │
   ▼
Incremental Processing
   │
   ▼
🥉 Bronze Parquet
   │
   ▼
🥈 Silver Parquet
   │
   ▼
🥇 Gold Parquet
```

This implementation demonstrates:

- SparkSession
- Spark DataFrames
- PySpark transformations
- Data type conversion
- NULL handling
- Duplicate removal
- Filtering
- Aggregations
- Watermark logic
- Incremental processing
- Parquet reads and writes
- Partitioning

---

# 📦 Parquet & Partitioning

The standalone PySpark implementation stores Bronze and Silver currency data as **Apache Parquet**.

The datasets are partitioned by:

```text
quote
```

Example:

```text
currency_rates/
│
├── quote=USD/
├── quote=GBP/
└── quote=CHF/
```

Partitioning organizes the dataset by currency and allows Spark to reduce unnecessary data scanning when filtering on the partition column.

---

# 🧱 Version 3 — Databricks Lakehouse

The latest implementation migrates the project to a modern **Databricks Lakehouse**.

It uses:

- Databricks
- PySpark
- Apache Spark
- Delta Lake
- Delta Tables
- Medallion Architecture
- Databricks Jobs
- Serverless Compute
- GitHub integration

Unlike the earlier Databricks version that focused only on currency data, the current implementation processes the complete **CRM + ERP + Currency** architecture.

---

# 🥉 Databricks Bronze Layer

The Databricks Bronze layer contains raw Delta Tables for the source systems.

## CRM

```text
bronze.crm_cust_info
bronze.crm_prd_info
bronze.crm_sales_details
```

## ERP

```text
bronze.erp_cust_az12
bronze.erp_loc_a101
bronze.erp_px_cat_g1v2
```

## Currency

```text
bronze.currency_rates
```

CRM and ERP data is ingested from CSV files using PySpark.

Currency data is retrieved from the REST API and loaded incrementally.

---

# 🔄 Currency Incremental Loading

The Currency API pipeline uses a **watermark**.

The watermark represents the latest date already available in Bronze.

```sql
SELECT MAX(date) AS watermark
FROM bronze.currency_rates
```

Conceptually:

```text
REST API
   │
   ▼
Incoming Rates
   │
   ▼
MAX(date) in Bronze
   │
   ▼
Watermark
   │
   ▼
date > watermark
   │
   ▼
Only New Records
   │
   ▼
Bronze Delta Table
```

If the Bronze table does not contain data yet, all available API records can be processed.

New records are appended to:

```text
bronze.currency_rates
```

---

# 🥈 Databricks Silver Layer

The Silver layer transforms the Bronze Delta Tables into cleaned and standardized datasets.

## CRM Silver Tables

```text
silver.crm_cust_info
silver.crm_prd_info
silver.crm_sales_details
```

### Customer Transformations

The CRM customer pipeline:

- Removes invalid customer IDs
- Keeps the latest customer record
- Trims customer names
- Standardizes marital status
- Standardizes gender

### Product Transformations

The CRM product pipeline:

- Extracts category IDs
- Standardizes product keys
- Replaces missing product costs
- Standardizes product lines
- Creates product validity periods

### Sales Transformations

The CRM sales pipeline:

- Converts order dates
- Converts shipping dates
- Converts due dates
- Corrects invalid sales amounts
- Corrects invalid prices

## ERP Silver Tables

```text
silver.erp_cust_az12
silver.erp_loc_a101
silver.erp_px_cat_g1v2
```

The ERP transformations include:

- Customer ID standardization
- Invalid future birthdate handling
- Gender standardization
- Country standardization
- Customer location cleaning
- Product-category preparation

## Currency Silver Table

```text
silver.currency_rates
```

Currency transformations include:

- Date conversion
- Numeric rate conversion
- Currency-code standardization
- Duplicate removal
- NULL validation
- Invalid exchange-rate validation

---

# 🥇 Databricks Gold Layer

The Gold layer integrates the cleaned CRM, ERP, and currency data into business-ready analytical tables.

## Customer Dimension

```text
gold.dim_customers
```

Combines CRM customer data with ERP customer and location information.

Contains attributes such as:

- Customer key
- Customer ID
- Customer number
- First name
- Last name
- Country
- Marital status
- Gender
- Birthdate
- Create date

## Product Dimension

```text
gold.dim_products
```

Combines CRM products with ERP product categories.

Contains:

- Product key
- Product ID
- Product number
- Product name
- Category
- Subcategory
- Cost
- Product line
- Start date

Only the current version of each product is included in the dimension.

## Sales Fact Table

```text
gold.fact_sales
```

Connects sales transactions with the Customer and Product dimensions.

Contains:

- Order number
- Product key
- Customer key
- Order date
- Shipping date
- Due date
- Sales amount
- Quantity
- Price

## Sales Currency Fact Table

```text
gold.fact_sales_currency
```

Integrates sales transactions with historical exchange rates.

The relationship is:

```text
fact_sales.order_date
        │
        ▼
currency_rates.date
```

Converted sales are calculated as:

```text
sales_amount × exchange_rate = converted_sales
```

This allows EUR sales to be analyzed in:

- USD
- GBP
- CHF

## Currency Summary

```text
gold.currency_summary
```

Provides analytical currency statistics:

- Average exchange rate
- Minimum exchange rate
- Maximum exchange rate

---

# ⭐ Databricks Star Schema

The final analytical model follows a Star Schema.

```text
                  dim_customers
                       │
                       │
                       ▼
dim_products ─────► fact_sales
                       │
                       ▼
              fact_sales_currency
                       │
                       ▼
              currency_rates
```

The model combines customer, product, sales, and historical exchange-rate information for analytics and reporting.

---

# 🔺 Why Delta Lake?

The Databricks implementation stores the Medallion layers using **Delta Tables**.

Conceptually:

```text
Delta Table
     =
Parquet Data
     +
Transaction Log
```

Delta Lake provides capabilities such as:

- ACID transactions
- Reliable writes
- UPDATE
- DELETE
- MERGE support
- Table versioning
- Transaction history
- Schema management

This makes Delta Lake suitable for managed Lakehouse workloads.

---

# ⚙️ Databricks Job Orchestration

The Databricks implementation contains automated workflows for both major pipelines.

## 💱 Currency Lakehouse Pipeline

```text
bronze_currency
      │
      ▼
silver_currency
      │
      ▼
gold_currency
```

This workflow automatically executes:

```text
REST API
   ↓
Watermark Check
   ↓
Incremental Bronze Load
   ↓
Silver Cleaning
   ↓
Gold Aggregation
```

## 🏢 CRM ERP Lakehouse Pipeline

The CRM and ERP pipeline is also fully orchestrated using Databricks Jobs.

```text
bronze_crm_erp
       │
       ▼
silver_crm_erp
       │
       ▼
gold_crm_erp
```

The workflow executes:

```text
CRM + ERP CSV Files
        │
        ▼
🥉 Bronze Delta Tables
        │
        ▼
🥈 Silver Transformations
        │
        ▼
🥇 Gold Star Schema
```

Task dependencies ensure that each layer starts only after the previous layer has completed successfully.

Both Databricks workflows have been successfully executed end-to-end.

---

# 📓 Databricks Notebooks

The Databricks implementation is organized into six notebooks.

## Bronze

```text
databricks/bronze/bronze_currency.ipynb
databricks/bronze/bronze_crm_erp.ipynb
```

### `bronze_currency.ipynb`

Responsible for:

- REST API ingestion
- Spark DataFrame creation
- Watermark retrieval
- Incremental filtering
- Bronze Delta loading

### `bronze_crm_erp.ipynb`

Responsible for:

- CRM CSV ingestion
- ERP CSV ingestion
- PySpark DataFrame creation
- Six Bronze Delta Tables

## Silver

```text
databricks/silver/silver_currency.ipynb
databricks/silver/silver_crm_erp.ipynb
```

### `silver_currency.ipynb`

Responsible for:

- Reading Bronze currency data
- Data type conversion
- Standardization
- Duplicate removal
- Data quality validation
- Silver Delta loading

### `silver_crm_erp.ipynb`

Responsible for:

- CRM customer cleaning
- CRM product transformation
- CRM sales cleaning
- ERP customer cleaning
- ERP location standardization
- ERP category preparation
- Silver Delta loading

## Gold

```text
databricks/gold/gold_currency.ipynb
databricks/gold/gold_crm_erp.ipynb
```

### `gold_currency.ipynb`

Responsible for creating:

```text
gold.currency_summary
```

### `gold_crm_erp.ipynb`

Responsible for creating:

```text
gold.dim_customers
gold.dim_products
gold.fact_sales
gold.fact_sales_currency
```

---

# 📂 Repository Structure

```text
data-engineering-lakehouse-project/
│
├── databricks/
│   │
│   ├── bronze/
│   │   ├── bronze_currency.ipynb
│   │   └── bronze_crm_erp.ipynb
│   │
│   ├── silver/
│   │   ├── silver_currency.ipynb
│   │   └── silver_crm_erp.ipynb
│   │
│   └── gold/
│       ├── gold_currency.ipynb
│       └── gold_crm_erp.ipynb
│
├── datasets/
│   │
│   ├── source_crm/
│   │   ├── cust_info.csv
│   │   ├── prd_info.csv
│   │   └── sales_details.csv
│   │
│   ├── source_erp/
│   │   ├── CUST_AZ12.csv
│   │   ├── LOC_A101.csv
│   │   └── PX_CAT_G1V2.csv
│   │
│   └── source_api/
│       └── currency_raw.json
│
├── python/
│   └── ingestion/
│       ├── load_data.py
│       └── currency_pipeline_pyspark.py
│
├── scripts/
│   │
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

# 🐍 Standalone Python Pipelines

The repository preserves the earlier Python implementations to demonstrate the project's technical evolution.

## `load_data.py`

The original implementation uses:

```text
Python
Pandas
SQLAlchemy
SQL Server
```

It demonstrates:

- REST API extraction
- Pandas processing
- Data quality validation
- SQL Server connectivity
- Watermark logic
- Incremental loading
- Stored procedure execution
- Logging
- Error handling

## `currency_pipeline_pyspark.py`

The standalone Spark implementation uses:

```text
Python
PySpark
Apache Spark
Apache Parquet
```

It demonstrates:

- SparkSession
- Spark DataFrames
- Data cleaning
- Data quality checks
- Watermark logic
- Incremental processing
- Parquet
- Partitioning
- Bronze processing
- Silver transformations
- Gold aggregations

---

# 🔄 Data Warehouse → Lakehouse Evolution

A major objective of this repository is to demonstrate how the same Data Engineering solution can evolve over time.

## Version 1

```text
Python
   ↓
Pandas
   ↓
SQL Server
   ↓
Bronze → Silver → Gold
```

## Version 2

```text
Python
   ↓
PySpark
   ↓
Parquet
   ↓
Bronze → Silver → Gold
```

## Version 3

```text
Databricks
   ↓
PySpark
   ↓
Delta Lake
   ↓
Bronze → Silver → Gold
   ↓
Databricks Jobs
```

The earlier implementations are intentionally preserved rather than replaced.

This makes it possible to see the progression from a traditional SQL-based Data Warehouse toward a modern Lakehouse implementation.

---

# 📊 Analytics Use Cases

The final Gold model supports multiple analytical use cases.

## Customer Analysis

- Customer purchasing patterns
- Customer contribution to revenue
- Customer geography
- Customer demographics

## Product Analysis

- Best-performing products
- Product categories
- Product subcategories
- Product sales performance

## Sales Analysis

- Revenue trends
- Sales over time
- Order analysis
- Product performance

## Currency Analysis

- Historical exchange rates
- Average exchange rates
- Minimum exchange rates
- Maximum exchange rates
- EUR → USD conversion
- EUR → GBP conversion
- EUR → CHF conversion
- Sales analysis across currencies

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
- Window Functions
- Joins
- Aggregations
- Parquet reads and writes
- Partitioning

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
- CSV Ingestion
- Data Quality
- Incremental Processing
- Watermark Logic
- Medallion Architecture
- Data Lakehouse
- Parquet
- Delta Lake
- Partitioning
- Multi-source Data Integration
- Dimensional Modeling
- Star Schema
- Pipeline Orchestration
- Logging
- Error Handling
- Git
- GitHub

---

# 🚀 Key Learning Outcomes

Through this project, I learned how to design, build, and evolve an end-to-end Data Engineering solution.

The project demonstrates how to:

1. Ingest data from CSV files and REST APIs.
2. Preserve raw API data as JSON.
3. Process data using Pandas and PySpark.
4. Build Spark DataFrames.
5. Clean and standardize source data.
6. Validate data quality.
7. Handle NULL values and duplicates.
8. Convert and validate data types.
9. Implement watermark logic.
10. Build incremental ingestion.
11. Store analytical data using Parquet.
12. Partition datasets.
13. Build Bronze, Silver, and Gold layers.
14. Create Delta Tables.
15. Build a Data Lakehouse.
16. Integrate CRM, ERP, and REST API data.
17. Build dimension tables.
18. Build fact tables.
19. Create a Star Schema.
20. Integrate historical currency rates with sales.
21. Build reusable Python/PySpark pipelines.
22. Separate Databricks processing into dedicated notebooks.
23. Configure Databricks task dependencies.
24. Orchestrate complete pipelines using Databricks Jobs.
25. Integrate Databricks with GitHub.
26. Migrate a traditional SQL Data Warehouse design to a Databricks Lakehouse.

---

# ✅ Current Project Status

The complete architecture has now been implemented.

```text
                    DATA SOURCES
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
       CRM CSV        ERP CSV       REST API
          │              │          Currency
          └──────────────┼──────────────┘
                         │
                         ▼
                    DATABRICKS
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
                    STAR SCHEMA
                         │
                         ▼
               ANALYTICS / REPORTING
```

### Completed

✅ SQL Server Data Warehouse  
✅ Python + Pandas pipeline  
✅ REST API ingestion  
✅ Raw JSON storage  
✅ Watermark logic  
✅ Incremental loading  
✅ PySpark pipeline  
✅ Parquet storage  
✅ Partitioning  
✅ Databricks Lakehouse  
✅ Delta Tables  
✅ CRM Databricks ingestion  
✅ ERP Databricks ingestion  
✅ Currency API Databricks ingestion  
✅ CRM/ERP Silver transformations  
✅ Currency Silver transformations  
✅ Gold dimensions  
✅ Gold fact tables  
✅ Star Schema  
✅ Historical currency integration  
✅ Currency Lakehouse Job orchestration  
✅ CRM ERP Lakehouse Job orchestration  
✅ GitHub integration  

---

# 🔜 Possible Future Improvements

The core project is complete, but possible future extensions include:

- Add scheduled Databricks Job runs
- Add more advanced pipeline monitoring
- Add automated data quality tests
- Add pipeline audit tables
- Add cloud object storage
- Explore Azure integration
- Build Power BI reporting on top of the Gold layer
- Explore CI/CD for Databricks deployments

These are possible extensions rather than requirements for the current project.

---

# 🛡️ License

This project is licensed under the **MIT License**.

See the `LICENSE` file for more information.
