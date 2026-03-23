# Databricks Medallion Parent-Child Pipeline

## 📌 Overview

This project demonstrates an end-to-end data engineering pipeline built using Databricks and AWS S3, implementing a medallion architecture (Bronze, Silver, Gold) with incremental data ingestion and multi-tenant (parent-child) data integration.

The pipeline processes raw child company data from S3, performs data cleaning and validation, and merges it into a structured parent-level Gold layer for analytics and reporting.

---

## 🏗️ Architecture Highlights

* S3-based ingestion using landing and processed zones
* Databricks processing pipelines for transformation and validation
* Medallion architecture (Bronze → Silver → Gold)
* Parent-child data model with schema alignment
* Incremental and full load strategies
* Daily scheduled job for automated data updates

---

## 🔄 Data Pipeline Flow

### Child Data Pipeline

1. Raw data lands in S3 (landing zone)
2. Data is ingested into Databricks
3. Files are moved to processed zone after ingestion
4. Bronze layer stores raw data
5. Silver layer applies validation and cleaning
6. Gold layer creates structured tables:

   * `sb_dim_customers`
   * `sb_dim_products`
   * `sb_dim_gross_price`
   * `sb_fact_orders`

---

## 🧹 Data Cleaning & Validation

* Duplicate removal
* Trimming whitespace
* Standardizing text casing
* Parsing `month` from multiple formats
* Validating `gross_price`:

  * Convert valid numeric values to double
  * Fix negative values (convert to positive)
  * Replace non-numeric values with 0

---

## 🔁 Incremental Processing Strategy

* Daily ingestion from S3 landing zone
* Processed files moved to S3 processed zone
* Incremental updates applied to fact tables
* Merge (UPSERT) into parent Gold layer

---

## 🏢 Parent Data Integration

* Parent Gold tables follow a dimensional model:

  * `dim_customers`
  * `dim_products`
  * `dim_date`
  * `dim_gross_price`
  * `fact_orders`

* Child Gold data is schema-aligned and merged into parent Gold tables

---

## ⏱️ Scheduling

* Pipeline is scheduled to run daily
* Automatically ingests new data and updates parent Gold layer

---

## 📊 Serving Layer

* Final Gold data is used for dashboards and analytics tools

---

## 🚀 Key Skills Demonstrated

* Databricks Lakehouse architecture
* Incremental ETL pipeline design
* Data cleaning and validation
* Dimensional modeling (fact & dimension tables)
* Multi-tenant data integration
* Workflow scheduling and automation

---
