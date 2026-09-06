# 🚕 Transportation Data Engineering Pipeline — GoodCabs

<p align="center">

**End-to-End Data Engineering | Databricks | PySpark | AWS | Delta Lake | SQL**

</p>


<p align="center">

[![Databricks](https://img.shields.io/badge/Databricks-EF3E42?style=for-the-badge\&logo=databricks\&logoColor=white)](https://www.databricks.com/)
[![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=for-the-badge\&logo=apachespark\&logoColor=white)](https://spark.apache.org/)
[![PySpark](https://img.shields.io/badge/PySpark-3776AB?style=for-the-badge\&logo=python\&logoColor=white)](https://spark.apache.org/docs/latest/api/python/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge\&logo=python\&logoColor=white)](https://www.python.org/)
[![SQL](https://img.shields.io/badge/SQL-336791?style=for-the-badge\&logo=postgresql\&logoColor=white)](https://www.w3schools.com/sql/)
[![AWS S3](https://img.shields.io/badge/AWS%20S3-569A31?style=for-the-badge\&logo=amazons3\&logoColor=white)](https://aws.amazon.com/s3/)
[![Delta Lake](https://img.shields.io/badge/Delta%20Lake-00ADD8?style=for-the-badge)](https://delta.io/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge\&logo=github\&logoColor=white)](https://github.com/)

</p>

---

<img width="1536" height="1024" alt="goodcabs project image" src="https://github.com/user-attachments/assets/c9c3c652-6b8a-4329-9dec-c002360288fd" />



## 📌 Project Summary

**GoodCabs Transportation Data Engineering Pipeline** is an end-to-end **Data Engineering project built on Databricks** to transform raw transportation data into clean, validated, and analytics-ready datasets.

The pipeline follows the **Medallion Architecture**:

```text
             RAW TRANSPORTATION DATA
                       │
                       ▼
                ┌────────────┐
                │   BRONZE   │
                │ Raw Data   │
                └──────┬─────┘
                       │
                       ▼
                ┌────────────┐
                │   SILVER   │
                │ Clean Data │
                └──────┬─────┘
                       │
                       ▼
                ┌────────────┐
                │    GOLD    │
                │ Analytics  │
                └──────┬─────┘
                       │
                       ▼
                 BI / REPORTING
```

The implementation uses **Databricks, PySpark, SQL, AWS S3, Delta Lake and Unity Catalog** to create a scalable Lakehouse-style data platform.

---

# 🎯 Business Problem

Transportation companies generate large volumes of trip data that can be difficult to use directly for reporting and analytics.

This project addresses the problem by creating a structured data pipeline that:

* Ingests transportation data
* Preserves raw source data
* Cleans and validates datasets
* Creates reusable dimensions
* Builds analytical fact tables
* Produces city-level datasets
* Enables downstream BI and reporting

---

# 🏗️ Architecture

## End-to-End Architecture

```text
┌───────────────────────────┐
│   Transportation System   │
└─────────────┬─────────────┘
              │
              ▼
┌───────────────────────────┐
│    Relational Database    │
└─────────────┬─────────────┘
              │
              ▼
┌───────────────────────────┐
│     Data Fetch Service    │
└─────────────┬─────────────┘
              │
              ▼
┌───────────────────────────┐
│          AWS S3           │
│      Raw Data Storage     │
└─────────────┬─────────────┘
              │
              ▼
╔════════════════════════════════════════╗
║              DATABRICKS                ║
║                                        ║
║  ┌──────────┐                          ║
║  │  BRONZE  │  Raw / Ingested Data     ║
║  └────┬─────┘                          ║
║       │                                ║
║       ▼                                ║
║  ┌──────────┐                          ║
║  │  SILVER  │  Clean / Validated Data  ║
║  └────┬─────┘                          ║
║       │                                ║
║       ▼                                ║
║  ┌──────────┐                          ║
║  │   GOLD   │  Business-Ready Data     ║
║  └────┬─────┘                          ║
║       │                                ║
╚═══════╪════════════════════════════════╝
        │
        ▼
┌───────────────────────────┐
│     BI / Analytics        │
│   Reporting / Dashboards  │
└───────────────────────────┘
```

---

# 🔄 Data Flow

```text
Source System
     ↓
Relational Database
     ↓
Data Extraction
     ↓
AWS S3
     ↓
Databricks
     ↓
Bronze Layer
     ↓
Silver Layer
     ↓
Gold Layer
     ↓
Analytics / BI
```

---

# 🥉 Bronze Layer

The Bronze layer stores **raw transportation data** received from the source system.

### Responsibilities

* Raw data ingestion
* Source data preservation
* Initial schema handling
* S3 data ingestion
* Preparing data for downstream processing

### Bronze Structure

```text
Bronze
└── trips
```

---

# 🥈 Silver Layer

The Silver layer transforms raw data into **clean, standardized and validated datasets**.

### Silver Tables

```text
Silver
├── calendar
├── city
└── trips
```

### Key Transformations

* Data cleansing
* Data type conversion
* Null handling
* Duplicate handling
* Data standardization
* Data validation
* Dimension creation
* Transformation of raw trip data

---

# 🥇 Gold Layer

The Gold layer contains **business-ready datasets** optimized for analytical workloads.

### Gold Tables

```text
Gold
├── fact_trips
├── fact_trips_chandigarh
├── fact_trips_coimbatore
├── fact_trips_indore
├── fact_trips_jaipur
├── fact_trips_kochi
├── fact_trips_lucknow
├── fact_trips_mysore
├── fact_trips_surat
├── fact_trips_vadodara
└── fact_trips_visakhapatnam
```

The implemented pipeline contains **11 Gold tables**, including the main `fact_trips` table and city-specific analytical datasets.

---

# 🧩 Data Model

```text
                    ┌─────────────┐
                    │   Calendar  │
                    │  Dimension  │
                    └──────┬──────┘
                           │
                           │
┌─────────────┐            ▼
│    City     │──────► fact_trips
│  Dimension  │            │
└─────────────┘             │
                            ▼
                    City-Level Tables
                            │
          ┌─────────────────┼─────────────────┐
          ▼                 ▼                 ▼
     Chandigarh        Coimbatore         Indore
          │                 │                 │
          └─────────────────┼─────────────────┘
                            ▼
                     Other Cities
```

This model supports both **overall transportation analysis** and **city-specific analytics**.

---

# 🔗 Databricks Data Lineage

The project uses Databricks lineage capabilities to track dependencies between datasets.

```text
Trips
  │
  ▼
Trips Silver Staging
  │
  ▼
Silver Trips
  │
  ├───────────────┐
  ▼               ▼
 City          Calendar
  │               │
  └───────┬───────┘
          ▼
      fact_trips
          │
          ├── Chandigarh
          ├── Coimbatore
          ├── Indore
          ├── Jaipur
          ├── Kochi
          ├── Lucknow
          ├── Mysore
          ├── Surat
          ├── Vadodara
          └── Visakhapatnam
```

The lineage provides visibility into the transformation flow from source datasets to analytical outputs.

---

# 📸 Screenshots & Project Evidence

> Add your actual Databricks screenshots to the `screenshots/` folder and update the filenames below.

## 🖥️ Databricks Workspace

<img width="1917" height="870" alt="Screenshot 2026-09-06 163856" src="https://github.com/user-attachments/assets/afd441cf-9125-409a-822f-a14737e2e2f6" />



Shows the Databricks project workspace and pipeline organization.

---

## 🔄 Databricks Pipeline

<img width="1917" height="866" alt="Screenshot 2026-09-06 171703" src="https://github.com/user-attachments/assets/439d550c-b233-4a62-bce8-59fa785dfd93" />



Shows the configured Databricks pipeline and execution flow.

---

## 🥉 Bronze Layer

<img width="1536" height="1024" alt="bronze layer image" src="https://github.com/user-attachments/assets/b3b87b35-c683-4a26-94a4-43aba9862a43" />



Raw transportation data ingestion.

---

## 🥈 Silver Layer

<img width="1536" height="1024" alt="silver layer image" src="https://github.com/user-attachments/assets/59e52e0d-f31d-4306-9c31-31b6c0b6bc9a" />



Cleaned and transformed datasets including:

* `calendar`
* `city`
* `trips`

---

## 🥇 Gold Layer

<img width="1536" height="1024" alt="gold layer image" src="https://github.com/user-attachments/assets/991334ca-6a20-4947-ac70-fb9cafacd096" />



Business-ready `fact_trips` and city-level analytical datasets.

---

## 🔗 Data Lineage

<img width="1536" height="1024" alt="Data Lineage" src="https://github.com/user-attachments/assets/eab4ff52-3e23-4d39-b2bf-a4b1397e35e8" />


Databricks lineage showing relationships between source, Silver and Gold datasets.

---

# 🧰 Technology Stack

| Technology           | Role                            |
| -------------------- | ------------------------------- |
| 🟧 **Databricks**    | Data Engineering Platform       |
| ⚡ **PySpark**        | Distributed Data Processing     |
| 🔥 **Apache Spark**  | Large-Scale Processing          |
| 🐍 **Python**        | Pipeline & Transformation Logic |
| 🗄️ **SQL**          | Data Transformation & Analytics |
| ☁️ **AWS S3**        | Cloud Object Storage            |
| 🧱 **Delta Lake**    | Reliable Data Storage           |
| 🔐 **Unity Catalog** | Governance & Data Management    |
| 🌳 **Git/GitHub**    | Version Control                 |

These technologies are the core stack documented for the implemented project.

---

# ⚙️ Pipeline Implementation

## Step 1 — Data Source

Transportation data originates from the source transportation system.

## Step 2 — Database

The source information is maintained in a relational database.

## Step 3 — Data Extraction

A data-fetch service extracts the required transportation data.

## Step 4 — AWS S3

Extracted data is stored in **Amazon S3**.

## Step 5 — Databricks

Databricks reads the incoming data and executes the transformation pipeline.

## Step 6 — Bronze

Raw data is loaded into the Bronze layer.

## Step 7 — Silver

Data is cleaned, validated and standardized.

## Step 8 — Gold

Fact and city-level analytical datasets are generated.

## Step 9 — Analytics

Gold datasets are prepared for BI, dashboards and reporting.

---

# 📊 Project Outputs

The final pipeline produces datasets suitable for:

### 🚕 Transportation Analytics

Analyze trip-related transportation data.

### 🏙️ City-Level Analysis

Analyze transportation performance across multiple cities.

### 📅 Date-Based Analysis

Support time and calendar-based reporting.

### 📈 Business Reporting

Provide structured datasets for business reporting.

### 📊 BI Dashboards

Enable downstream dashboard and visualization development.

The Gold layer is specifically designed for analytics, transportation KPIs, reporting and dashboard consumption.

---

# 🧠 Key Data Engineering Skills Demonstrated

```text
✅ ETL / ELT
✅ Data Pipeline Development
✅ Databricks
✅ PySpark
✅ Apache Spark
✅ SQL
✅ AWS S3
✅ Delta Lake
✅ Unity Catalog
✅ Medallion Architecture
✅ Lakehouse Architecture
✅ Data Transformation
✅ Data Cleansing
✅ Data Validation
✅ Data Quality
✅ Data Lineage
✅ Fact & Dimension Modeling
✅ Analytics-Ready Data
```

---

# 📂 Repository Structure

```text
DE-Transportation-GoodCabs/
│
├── README.md
│
├── databricks/
│   │
│   ├── bronze/
│   │   └── bronze_trips.py
│   │
│   ├── silver/
│   │   ├── silver_trips.py
│   │   ├── silver_city.py
│   │   └── silver_calendar.py
│   │
│   └── gold/
│       ├── fact_trips.py
│       └── city_fact_tables.py
│
├── pipelines/
│   └── transportation_pipeline/
│
├── sql/
│   └── analytics_queries.sql
│
├── docs/
│   └── architecture/
│       └── transportation-pipeline.png
│
├── screenshots/
│   ├── databricks_workspace.png
│   ├── databricks_pipeline.png
│   ├── bronze_layer.png
│   ├── silver_layer.png
│   ├── gold_layer.png
│   └── databricks_lineage.png
│
└── .gitignore
```

---

# 🚀 Key Features

* ✔️ End-to-end cloud data pipeline
* ✔️ Medallion Architecture
* ✔️ Bronze → Silver → Gold processing
* ✔️ Distributed processing with PySpark
* ✔️ Delta Lake-based data storage
* ✔️ AWS S3 integration
* ✔️ Data quality and validation
* ✔️ Fact & dimension modeling
* ✔️ City-level analytical datasets
* ✔️ Databricks Data Lineage
* ✔️ Analytics-ready Gold layer

---

# 🎯 Project Objectives

1. Build a scalable transportation data pipeline.
2. Ingest source data into AWS S3.
3. Process data using Databricks and PySpark.
4. Implement Bronze, Silver and Gold layers.
5. Perform data cleansing and validation.
6. Create reusable fact and dimension datasets.
7. Implement Delta Lake for reliable data storage.
8. Utilize Unity Catalog for data governance.
9. Create city-level analytical datasets.
10. Prepare analytics-ready datasets for BI consumption.

---

# 🔐 Security

**Never commit sensitive credentials to GitHub.**

Do not upload:

```text
❌ AWS Access Keys
❌ AWS Secret Keys
❌ Databricks Tokens
❌ Passwords
❌ API Keys
❌ Database Credentials
❌ Connection Strings
```

Use environment variables, secret scopes or other secure credential-management mechanisms.

---


## 📬 Contact

**Tanveer Kakar**
Data Engineer | Python | SQL | PySpark | Databricks | AWS

📌 Open to **Data Engineer / Junior Data Engineer opportunities**.

---

<p align="center">

### 🚕 Built with Databricks • PySpark • AWS • Delta Lake • SQL

**Bronze → Silver → Gold → Analytics**

</p>
