# Azure-data-engineering-Australia-Health-data

## Project Overview

This project demonstrates an end-to-end **Azure Data Engineering pipeline** built using modern cloud tools to process and analyze **Australia Health Expenditure Data**.  The pipeline extracts source data, performs transformations using Databricks, stores processed data in multiple layers, and visualizes using Power BI for business decision-making

## Architecture

```text
Source Data
   ↓
Azure Data Factory
   ↓
Azure Databricks
   ├── Raw Layer
   ├── Clean Layer
   ├── Curated Layer
   ↓
Power BI Dashboard
   ↓
Business Decision Making
