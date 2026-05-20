# Enterprise SCD Type 2 Pipeline using Azure Data Factory

## Project Overview

This project demonstrates an **enterprise-level Slowly Changing Dimension Type 2 (SCD Type 2)** implementation using:

* Microsoft Azure Data Factory (ADF)
* Mapping Data Flows
* Azure Data Lake Storage Gen2 (ADLS Gen2)
* CSV Source Files
* Parquet Target Files

The solution dynamically handles both:

* Initial Load
* Incremental Load

using a **single master pipeline**.

The project is designed based on real-world **investment banking client account tracking** requirements where historical data preservation is critical for:

* Audit reporting
* Regulatory compliance
* Risk analysis
* KYC tracking
* Historical analytics

---

# Key Features

* Enterprise-style SCD Type 2 implementation
* Dynamic Initial vs Incremental Load Handling
* Single Master Pipeline Architecture
* Hash-Based Change Detection
* Historical Data Preservation
* Mapping Data Flow Transformations
* Data Quality Validation using Assert Transformation
* Automatic Record Expiry Logic
* Current Record Tracking
* File-Based Data Warehouse Design
* Parquet Optimization for Analytics

---

# Architecture Overview

<img width="1066" height="1475" alt="ChatGPT Image May 20, 2026, 09_35_17 PM" src="https://github.com/user-attachments/assets/df3c7993-cfc1-4ba0-b73b-8b022d5b5c27" />


---

# Master Pipeline Design

Pipeline Name:

```text
PL_Master_Client_SCD2_Load
```

Activities Used:

* Get Metadata Activity
* If Condition Activity
* Execute Data Flow Activity

Dynamic Logic:

| Condition             | Action                    |
| --------------------- | ------------------------- |
| Target Exists = FALSE | Run Initial Load          |
| Target Exists = TRUE  | Run Incremental SCD2 Load |

---

# SCD Type 2 Business Logic

The pipeline preserves historical changes instead of overwriting existing records.

## Example

### Before Change

| client_id | risk_category | is_current |
| --------- | ------------- | ---------- |
| 1001      | Medium        | Y          |

### After Change

| client_id | risk_category | is_current |
| --------- | ------------- | ---------- |
| 1001      | Medium        | N          |
| 1001      | High          | Y          |

This ensures complete historical tracking.

---

# Technologies Used

| Technology                   | Purpose           |
| ---------------------------- | ----------------- |
| Microsoft Azure Data Factory | ETL Orchestration |
| ADLS Gen2                    | Storage Layer     |
| Mapping Data Flow            | Transformations   |
| CSV                          | Source Format     |
| Parquet                      | Target Format     |
| SHA2 Hashing                 | Change Detection  |

---

# ADLS Gen2 Folder Structure

```text
ADLS Gen2
│
├── source
│   ├── day 1
│   └── day 2
│
├── sink
│   └── dim_client_accounts
│
├── error
│
└── archive
```

---

# Incremental Load Flow

<img width="849" height="1008" alt="image" src="https://github.com/user-attachments/assets/885c9cf5-a77a-4b14-9e15-cdc3153cb4e3" />

<img width="959" height="437" alt="Screenshot 2026-05-20 203457" src="https://github.com/user-attachments/assets/1ce276e0-9964-4734-b2de-fda038fdd9fc" />
<img width="924" height="395" alt="Screenshot 2026-05-20 203140" src="https://github.com/user-attachments/assets/0ecf948a-fdc9-4dee-918a-95c50f67a0c6" />
<img width="926" height="412" alt="Screenshot 2026-05-20 203021" src="https://github.com/user-attachments/assets/6377b3f5-b9ad-49ef-a418-c0759d0bace4" />








---

# Important SCD2 Columns

| Column               | Purpose                    |
| -------------------- | -------------------------- |
| surrogate_key        | Unique version identifier  |
| effective_start_date | Record active start date   |
| effective_end_date   | Record expiry date         |
| is_current           | Active record indicator    |
| hash_key             | Change detection mechanism |

---

# Data Quality Validation

Implemented using:

* Assert Transformation
* Null Checks
* Mandatory Field Validation
* Reject Row Handling

---

# Performance Optimizations

* Parquet Format
* Hash Comparison Logic
* Broadcast Join
* Filtering Current Records Only
* Schema Drift Handling

---

# Production Best Practices Implemented

* Dynamic Pipeline Design
* Reusable Architecture
* Historical Preservation
* Error Handling
* Monitoring Support
* Scalable Design Pattern

---

# Common Business Use Cases

* Investment Banking
* Risk Management
* Regulatory Reporting
* Customer Master Data
* KYC Tracking
* Historical Audit Reporting

---

# Future Enhancements

* Delta Lake Migration
* CDC-Based Incremental Loads
* Metadata-Driven Framework
* Real-Time Streaming Architecture
* Databricks Integration

---

# Learning Outcomes

This project demonstrates practical experience in:

* SCD Type 2 Design
* Azure Data Factory
* Mapping Data Flows
* Enterprise ETL Design
* Historical Data Warehousing
* Data Lake Architecture
* Incremental Processing
* Change Data Detection

---

# Author

**Sai Shiva**
Azure Data Engineering | ETL | ADF | Databricks | PySpark | SQL

---

# License

This project is for educational and portfolio demonstration purposes.

