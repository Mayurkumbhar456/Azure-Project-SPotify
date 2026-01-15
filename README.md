# 🎵 End-to-End Spotify Data Engineering Project on Azure

## 📌 Project Overview
This project demonstrates an end-to-end Data Engineering pipeline built using **Microsoft Azure** and **Databricks**. It covers the complete data journey from ingestion to serving, utilizing modern practices like **Medallion Architecture**, **Delta Live Tables (DLT)**, and **CI/CD with Databricks Asset Bundles**.

The goal is to analyze Spotify simulation data (Users, Artists, Tracks, Streams) implementing **Slowly Changing Dimensions (SCD)** and real-time processing capabilities.

---

## 🏗️ Architecture & Tech Stack

**Cloud Provider:** Microsoft Azure  
**Core Technologies:**
* **Ingestion & Orchestration:** Azure Data Factory (ADF), Logic Apps
* **Storage:** Azure Data Lake Gen2 (ADLS), Azure SQL DB
* **Processing & Transformation:** Azure Databricks, PySpark, Spark Structured Streaming
* **Data Governance:** Databricks Unity Catalog
* **DevOps:** Databricks Asset Bundles (DAB), GitHub Actions (CI/CD)

---

## 🚀 Key Features & Implementation Details

### 1. Data Ingestion & Orchestration (Azure Data Factory)
* **Incremental Ingestion:** Designed pipelines to handle incremental data loads from Azure SQL DB to ADLS Gen2.
* **Backfilling Mechanism:** Implemented logic to handle historical data backfilling seamlessly.
* **Control Flow:** Used `Lookup` and `ForEach` activities to loop through metadata and trigger dynamic pipelines.
* **Alerting:** Integrated **Azure Logic Apps** to send email notifications upon pipeline success or failure.

### 2. Data Lakehouse Architecture (Databricks)
* **Medallion Architecture:**
    * **Bronze:** Raw data ingestion using **Autoloader** (Schema evolution & efficient file listing).
    * **Silver:** Cleaned, deduplicated, and enriched data. Implemented **SCD Type 1 and Type 2** for dimension tables (Users, Artists).
    * **Gold:** Aggregated business-level tables ready for analytics (Star Schema).
* **Unity Catalog:** Centralized governance for all data assets.

### 3. Advanced Transformation & Automation
* **Delta Live Tables (DLT):** Built declarative pipelines for quality constraints and automated lineage.
* **Metadata-Driven Pipelines:** utilized **Jinja Templates** in PySpark to create reusable code blocks for similar datasets.
* **Spark Structured Streaming:** Enabled low-latency data processing.

### 4. CI/CD & Deployment
* **Databricks Asset Bundles (DAB):** Configuration-as-code approach for deploying jobs and pipelines across Dev, Staging, and Prod environments.

---

## 📂 Repository Structure

```text
├── src/
│   ├── silver/                 # Transformation logic for Silver layer (Dimensions)
│   ├── gold/                   # Aggregation logic for Gold layer
│   └── dlt/                    # Delta Live Tables pipelines
├── utils/                      # Helper Python functions
├── Jinja/                      # Jinja templates for dynamic query generation
├── resources/                  # Databricks resource configurations (Job definitions)
├── databricks.yml              # Bundle configuration
└── spotify_incremental_load.sql # SQL scripts for simulating data updates
