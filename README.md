# Azure Data Engineering Project - Australia Health & Population Data Pipeline

## Project Overview

This project demonstrates an end-to-end Azure Data Engineering pipeline built to process and analyze **Australian Health Expenditure and Population Data**.

The pipeline uses **Azure Data Factory (ADF)** for ingestion, **Databricks (PySpark)** for transformation, and **Power BI** for analytics, following a **medallion architecture (Raw → Clean → Curated)**.

---

## Architecture Flow

```id="flow123"
HTTP Source (CSV Files)
    ↓
Azure Data Factory Pipeline (Parameterized)
    ↓
Azure Data Lake Storage (Raw Layer)
    ↓
Azure Databricks (Transformation)
    ├── Clean Layer
    ├── Curated Layer
    ↓
Power BI Dashboard
```

---

## ADF Pipeline Architecture

![Screenshots](Project-Diagram.png)
![Screenshots](Extract - Copy activity.png)

### Key Components Used

1. **Linked Services**

   * `ls_http_auhealthexpend23_source` → HTTP source connection
   * `ls_adls_auhealthexpend23dll` → ADLS Gen2 connection

2. **Datasets**

   * `ds_auhealthexpend23_raw_csv_http` → Source dataset (CSV via HTTP)
   * `ds_auhealthexpend23_raw_csv_dl` → Sink dataset (ADLS CSV)

3. **Pipeline**

   * `pl_extract_auhealthexpend_source_data`

4. **Activities**

   * **ForEach Activity**

     * Iterates over multiple files from parameter JSON
   * **Copy Activity**

     * Copies data from HTTP → ADLS (Raw Layer)

---

## Parameterization (Dynamic Pipeline)

A parameter file is used to drive ingestion dynamically:

* **Storage:** Blob Storage
* **File:** `source_file_list.json`
* **Dataset:** `ds_auhealthexpend23_file_list_sa`
* **Linked Service:** `ls_ablob_auhealthexpend23sa`

### Benefits:

* Scalable ingestion for multiple files
* No hardcoding of file names
* Easy to extend pipeline

---

## Tech Stack

* Azure Data Factory
* Azure Databricks
* PySpark
* Azure Data Lake Storage (ADLS Gen2)
* SQL
* Power BI

---

## Dataset Information

### 1. Health Expenditure Dataset

**File:** `australian_health_expenditure.csv`

Includes:

* Year
* Jurisdiction (State)
* Sector
* Area of expenditure
* Funding sources
* Current & constant expenditure amounts

---

### 2. Population Dataset

**File:** `australian_population_by_state.csv`

Includes:

* Time
* State-wise population
* Total population

---

## Project Workflow

### 1. Data Ingestion (ADF)

* Data pulled from HTTP source
* Parameter-driven ingestion using JSON
* ForEach loop processes multiple files
* Data stored in ADLS Raw Layer

---

### 2. Raw Layer

* Stores original CSV files
* Maintains source integrity
* Supports reprocessing

---

### 3. Clean Layer (Databricks - PySpark)

#### Transformations:

* Removed nulls and duplicates
* Renamed columns
* Converted data types
* Standardized formats
* Unpivoted population dataset

---

### 4. Curated Layer

Created analytical datasets:

* State-wise expenditure aggregation
* Funding source analysis
* Population trends
* **Per capita healthcare expenditure (key metric)**

---

### 5. Power BI Dashboard

Visualizations include:

* Healthcare spending trends
* State-wise comparison
* Funding breakdown
* Population vs expenditure
* Per capita analysis

---

## Business Problem

Healthcare organizations need insights into how funds are allocated and utilized.

### Key Questions Answered:

* Which states receive the most funding?
* How does spending vary across sectors?
* Who are the major contributors?
* How does population impact healthcare spending?

---

## Key Features

* Parameterized ADF pipeline
* ForEach + Copy Activity implementation
* Multi-source ingestion
* Medallion architecture
* Scalable cloud pipeline
* Business-ready analytics

---

## Skills Demonstrated

* Azure Data Factory (Linked Services, Datasets, Pipelines)
* Parameterization & Dynamic Pipelines
* Azure Databricks (PySpark)
* Data Transformation & Modeling
* SQL
* Power BI
* ETL/ELT Design

---

## Repository Structure

```id="repo321"
azure-health-data-project/
│
├── adf-pipelines/
│   ├── pipeline.json
│   ├── linked-services/
│   ├── datasets/
│
├── databricks-notebooks/
├── datasets/
│   ├── australian_health_expenditure.csv
│   ├── australian_population_by_state.csv
│
├── powerbi-dashboard/
├── architecture-diagram/
│   └── Extract - Copy activity.png
│
├── README.md
```

---

## Future Improvements

* Incremental load using watermark
* Auto Loader for streaming ingestion
* CI/CD with Azure DevOps
* Synapse Analytics integration
* ML-based forecasting

---

## Author

**Your Name**

* LinkedIn Profile
* GitHub Profile
