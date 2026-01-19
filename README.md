# ATP Tennis Analytics Pipeline (Databricks)

## Overview
This project implements an **end-to-end Medallion Architecture (Bronze → Silver → Gold)** data pipeline in **Databricks** using **PySpark** and **Delta Lake**.  
ATP tennis match, player, and ranking data is stored in **Azure Data Lake Storage (ADLS)** and transformed into analytics-ready fact and dimension tables.

All notebooks are orchestrated and **scheduled as a Databricks Job pipeline** for automated execution.

---

## Architecture
Bronze (Raw CSVs in ADLS)
↓
Silver (Cleaned & Normalized Delta Tables)
↓
Gold (Analytics-Ready Fact & Dimension Tables)

## Repository Structure
```text
.
├── bronze_layer.ipynb   # Raw data ingestion & exploration
├── silver_layer.ipynb   # Data cleansing, normalization & quality checks
├── gold_layer.ipynb     # Business logic, facts & dimensions
└── README.md
