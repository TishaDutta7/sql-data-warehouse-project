# SQL Data Warehouse Project (Medallion Architecture)

This project demonstrates the design and implementation of a **modern SQL-based Data Warehouse** using the **Medallion Architecture (Bronze, Silver, Gold)**.  
It covers end-to-end data ingestion, transformation, data quality checks, and analytical modeling using **SQL Server (T-SQL)**.

---

## 📊 Data Architecture & Flow

<img width="3072" height="1552" alt="image" src="https://github.com/user-attachments/assets/b15cd92e-56c8-4ff2-9dce-298304b11d41" />

> **Note:**  
> - Source systems provide raw CSV files  
> - Data flows through Bronze → Silver → Gold layers  
> - Gold layer exposes business-ready views for analytics and reporting  

---

## 📘 Project Overview

This project involves:

1. **Data Architecture**  
   - Designing a modern data warehouse using the **Medallion Architecture**
   - Clear separation of raw, cleansed, and business-ready data

2. **ETL Pipelines**  
   - Extracting data from CSV-based CRM and ERP source systems  
   - Transforming and loading data using SQL Server stored procedures

3. **Data Modeling**  
   - Designing **fact and dimension views** using a Star Schema
   - Optimized for analytical queries and BI tools

4. **Analytics & Reporting**  
   - Supporting ad-hoc SQL analysis
   - Enabling downstream BI & Machine Learning use cases

---

## 🔹 Bronze Layer (Raw Data)

**Purpose:**  
Stores raw data as-is from the source systems.

**Implementation Details:**
- Object Type: Tables
- Load Type:
  - Batch processing
  - Full load
  - Truncate & Insert
- No transformations applied
- Stored Procedure: `bronze.load_bronze`

**Key Responsibilities:**
- Ingest CSV files using `BULK INSERT`
- Preserve source data fidelity

---

## 🔹 Silver Layer (Cleansed & Standardized Data)

**Purpose:**  
Prepares clean, consistent, and analysis-ready data.

**Implementation Details:**
- Object Type: Tables
- Stored Procedure: `silver.load_silver`

**Operations Performed:**
- Data cleansing & normalization
- Deduplication using window functions
- Data validation and corrections
- Business rule enforcement

**Key Transformations:**
- Trimming and standardizing string fields
- Mapping coded values to descriptive values  
  *(e.g., gender, marital status, product line)*
- Handling invalid and future dates
- Recalculating derived metrics  
  *(sales = quantity × price)*
- Selecting latest records using `ROW_NUMBER()`

---

## 🔹 Gold Layer (Business-Ready Data)

**Purpose:**  
Provides analytics-ready datasets modeled using a **Star Schema**.

**Implementation Details:**
- Object Type: Views
- No physical data duplication
- Optimized for reporting and BI tools

**Gold Objects:**
- `gold.dim_customers`
- `gold.dim_products`
- `gold.fact_sales`

**Characteristics:**
- Clean, enriched, and business-aligned data
- Easy to query for analytics and dashboards

---

## ✅ Data Quality Checks

Comprehensive quality checks are implemented after the Silver layer load to ensure:

- No duplicate or NULL primary keys
- Proper trimming of string fields
- Valid date ranges and correct date ordering
- Correct sales calculations  
  *(sales = quantity × price)*
- Standardized categorical values across datasets

---

## 🛠️ Technology Stack

- **Database:** SQL Server
- **Language:** T-SQL
- **ETL:** Stored Procedures
- **Modeling:** Star Schema
- **Architecture:** Medallion (Bronze, Silver, Gold)

---

## 🚀 How to Run

1. Create the database and schemas (`bronze`, `silver`, `gold`)
2. Load raw data:
   ```sql
   EXEC bronze.load_bronze;
