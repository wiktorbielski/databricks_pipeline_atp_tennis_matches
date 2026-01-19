# 🎾 ATP Tennis Data Pipeline – Databricks Medallion ETL

A **Bronze → Silver → Gold** ETL pipeline for ATP tennis data using **Databricks, PySpark, and Delta Lake**.  
Ingests raw CSVs, cleans data, applies quality checks, and produces analytics-ready tables. The pipeline is fully **orchestrated and scheduled using Databricks Jobs**.

---

## 🏗️ Pipeline Overview

**Pipeline Flow:**
- **Bronze**: Raw CSVs from [JeffSackmann/tennis_atp](https://github.com/JeffSackmann/tennis_atp)
  - Raw data ingestion, minimal transformations
- **Silver**: Cleaned & validated Delta tables
  - Standardization, QA checks, partitioned by year
- **Gold**: Fact & Dimension tables for analytics
  - Enriched matches, players, rankings; derived metrics
 
**Orchestration:**  
- Fully automated via Databricks Jobs
- Scheduled daily at 08:00 Europe/Warsaw time
- Tasks executed sequentially: `bronze_layer → silver_layer → gold_layer`
- Retry logic and cluster configuration defined in `job_configuration_structure.yaml`

## 📂 Repository

| Layer | Description | Link |
|-------|------------|------|
| Bronze | Raw ATP CSV ingestion | [bronze_layer.ipynb](https://github.com/wiktorbielski/databricks_pipeline_atp_tennis_matches/blob/main/bronze_layer.ipynb) |
| Silver | Data cleansing, normalization, QA checks | [silver_layer.ipynb](https://github.com/wiktorbielski/databricks_pipeline_atp_tennis_matches/blob/main/silver_layer.ipynb) |
| Gold | Analytics-ready fact & dimension tables | [gold_layer.ipynb](https://github.com/wiktorbielski/databricks_pipeline_atp_tennis_matches/blob/main/gold_layer.ipynb) |
| Docs | Column definitions | [matches_data_dictionary.txt](https://github.com/wiktorbielski/databricks_pipeline_atp_tennis_matches/blob/main/matches_data_dictionary.txt) |
| Jobs | Databricks job structure | [job_configuration_structure.yaml](https://github.com/wiktorbielski/databricks_pipeline_atp_tennis_matches/blob/main/job_configuration_structure.yaml) |

---

## ⚡ Key Features

- **Bronze Layer**
  - Ingests raw ATP CSVs from [JeffSackmann/tennis_atp](https://github.com/JeffSackmann/tennis_atp)
  - Stores original data for traceability and reproducibility
  - Minimal transformations; all raw columns preserved
  - **Acknowledgment:** Thanks to Jeff Sackmann for compiling and maintaining this dataset.

- **Silver Layer**
  - Cleans and standardizes matches, players, and rankings
  - Partitioned by year
  - Performs **data quality checks**:
    - Completeness (mandatory columns)
    - Uniqueness (duplicate matches)
    - Referential integrity (winner ≠ loser, valid ranks)
    - Temporal checks (future dates, year consistency)

- **Gold Layer**
  - **fact_singles_matches** – One row per match; enriched with player info and ranking; derived metrics like `is_upset` and `rank_diff`
  - **dim_players** – One row per player; includes `full_name`, `is_left_handed`, height, IOC, DOB, Wikidata ID
  - **fact_player_rankings** – One row per player per ranking date; calculates `rank_change` and `points_change`

---

## 🛠️ Tech Stack

- Databricks / PySpark
- Delta Lake
- Azure Data Lake Storage Gen2
- YAML for job configuration
