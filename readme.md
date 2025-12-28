# Drug-API-Integrator

## Overview

**Drug-API-Integrator** is a data science project that focuses on integrating heterogeneous drug data from multiple healthcare APIs into a unified and high-quality dataset for analysis. The project demonstrates a full **data science pipeline** including **data acquisition, storage, integration, profiling, quality assessment, and basic analysis**.  

The main **research question** driving this project is:

> *"How can heterogeneous drug data from multiple healthcare APIs be effectively integrated into a unified and high-quality dataset for analysis?"*

This project uses real-world APIs and demonstrates how automated data integration and quality checks can be applied to healthcare datasets.

---

## Data Sources

1. **RxNorm API** – Provides standardized drug identifiers (RxCUI) and drug information.  
2. **OpenFDA API** – Provides drug warnings, purposes, and safety information.  
3. **Synthetic/Generated Data** – Simulated additional drug entries to enrich the dataset for analysis and integration exercises.

---

## Project Workflow

The project covers all phases of a typical **data science pipeline**:

1. **Data Acquisition**  
   - Fetch data from RxNorm and OpenFDA APIs using Python (`requests`)  
   - Save raw data locally in JSON format  

2. **Data Storage**  
   - Store integrated drug data in an **SQLite database** (`medicine.db`)  
   - Table: `drug_data` with columns:  
     - `id` (Primary Key)  
     - `drug_name`  
     - `rxcui`  
     - `openfda_warnings`  
     - `openfda_purpose`  

3. **Data Integration / Enrichment**  
   - Merge API datasets with synthetic drug entries  
   - Handle missing values and data inconsistencies  
   - Automate the integration process in Python  

4. **Data Profiling / Quality Assessment**  
   - Check for missing values and duplicates  
   - Remove duplicate records in SQL  
   - Ensure data completeness and consistency  

5. **Data Analysis**  
   - Example SQL/Pandas queries:
     - Count drugs per `openfda_warnings`  
     - Count drugs per `openfda_purpose`  
     - Identify drugs with missing `rxcui`  
   - Generate insights on the integrated drug dataset  

6. **Automation / Reproducibility**  
   - Entire pipeline can be run using Python scripts or a Jupyter notebook  
   - Ensures repeatable and scalable workflow  

---

## Example Queries

```sql
-- Count drugs per warning
SELECT openfda_warnings, COUNT(*) as count
FROM drug_data
GROUP BY openfda_warnings;

-- Count drugs per purpose
SELECT openfda_purpose, COUNT(*) as count
FROM drug_data
GROUP BY openfda_purpose;

-- Retrieve 20 drugs with missing RxCUI
SELECT * FROM drug_data
WHERE rxcui IS NULL
LIMIT 20;
