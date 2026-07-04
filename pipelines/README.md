# Data Factory Pipelines

This folder contains exported JSON definitions of the Data Factory pipelines built in Microsoft Fabric for this project. Sensitive identifiers (workspace ID, warehouse endpoint, object ID) have been redacted before publishing.

## `Pipeline_load_data_from_files_to_tables.json`
**Bronze layer — Files → Lakehouse Tables**

Copies raw CSV files from the Lakehouse `Files` section and loads them into Delta tables within the Lakehouse `Tables` section.

- **Source:** Delimited text (CSV) files in the Lakehouse
- **Sink:** Lakehouse Delta table (append)
- **Example activity:** `Copy data dim_dish` — loads `dim_dish.csv` into the `dim_dish_new` Lakehouse table

## `pipeline_lw_to_dw.json`
**Silver/Gold layer — Lakehouse → Data Warehouse**

Copies the dimension and fact tables from the Lakehouse into the Data Warehouse, where the Star Schema is modeled.

- **Source:** Lakehouse Delta tables
- **Sink:** Data Warehouse tables (auto-create, insert, staged copy)
- **Tables moved:**
  - `dim_date`
  - `dim_location`
  - `dim_dish`
  - `dim_restaurant`
  - `fact_orders`

Together, these two pipelines form the orchestration layer of the Medallion Architecture described in the main [README](../README.md), moving data from raw CSVs all the way into the warehouse-ready Star Schema used by the Power BI report.
