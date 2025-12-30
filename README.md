📊 SQL Data Warehouse Project (Medallion Architecture)

End-to-end SQL Data Warehouse implementation using Medallion Architecture (Bronze, Silver, Gold) on SQL Server.
This project demonstrates real-world data engineering concepts including ETL pipelines, data cleansing, validation, and star schema modeling for analytics and reporting.

🏗️ Data Warehouse Architecture
<img width="3072" height="1552" alt="image" src="https://github.com/user-attachments/assets/5daf0657-394c-48b8-92da-1892c44db42e" />

📌 Project Overview

This project implements a modern data warehouse using SQL Server and follows the Medallion Architecture pattern:

Bronze Layer → Raw data ingestion

Silver Layer → Cleaned & standardized data

Gold Layer → Business-ready analytical views (Star Schema)

The pipeline ingests data from CRM and ERP CSV sources, processes it through multiple transformation layers, and exposes fact and dimension views for reporting and analytics.

🏗️ Architecture Overview
Medallion Architecture Layers

Bronze Layer

Stores raw data as-is from source systems

Data ingested from CSV files using BULK INSERT

No transformations applied

Schema: bronze

Silver Layer

Cleanses, standardizes, and normalizes data

Handles:

Deduplication

Null handling

Data standardization (gender, country, product lines, dates)

Business rule validation

Schema: silver

Gold Layer

Business-ready analytical layer

Implements Star Schema

Optimized for BI & reporting

Schema: gold

🗂️ Data Flow (Lineage)

Sources → Bronze → Silver → Gold → Consumption

Sources

CRM (Customer, Product, Sales)

ERP (Customer, Location, Product Category)

Consumption

BI & Reporting

Ad-hoc SQL queries

Machine Learning (future-ready)

🧱 Data Model (Gold Layer)
Dimensions

gold.dim_customers

gold.dim_products

Fact

gold.fact_sales

The Gold layer is modeled using a Star Schema, enabling efficient analytical queries and reporting.

⚙️ ETL Implementation
Bronze Layer

Stored Procedure: bronze.load_bronze

Operations:

Truncate tables

Load CSV files using BULK INSERT

Batch processing

Silver Layer

Stored Procedure: silver.load_silver

Operations:

Data cleansing & normalization

Deduplication using window functions

Data validation and corrections

Business rule enforcement

Gold Layer

Implemented using SQL Views

Combines Silver data into analytical dimensions and fact views

No physical data duplication

✅ Data Quality Checks

Quality checks are implemented to ensure:

No duplicate or NULL primary keys

Proper trimming of string fields

Valid date ranges

Correct sales calculations (sales = quantity × price)

Consistent standardization values

These checks help maintain data reliability and trust.

🛠️ Tech Stack

Database: Microsoft SQL Server

Language: T-SQL

Architecture: Medallion (Bronze / Silver / Gold)

Data Sources: CSV files (CRM & ERP)

Modeling: Star Schema

Documentation: GitHub + Draw.io

📁 Repository Structure
├── bronze/
│   ├── ddl_bronze_tables.sql
│   └── sp_load_bronze.sql
│
├── silver/
│   ├── ddl_silver_tables.sql
│   ├── sp_load_silver.sql
│   └── quality_checks.sql
│
├── gold/
│   └── gold_views.sql
│
├── datasets/
│   ├── source_crm/
│   └── source_erp/
│
├── docs/
│   └── data_flow.png
│
└── README.md

🎯 Key Learnings & Highlights

Real-world ETL pipeline design

Data cleansing & validation strategies

SQL-based dimensional modeling

End-to-end data warehouse implementation

Production-style logging and error handling

📌 Future Enhancements

Incremental loading (CDC)

Orchestration using Airflow / SQL Agent

BI dashboards (Power BI / Tableau)

Performance optimization & indexing

👤 Author

Tisha Dutta
