# 🍔 Swiggy Sales Intelligence Dashboard: An End-to-End Microsoft Fabric Pipeline

An end-to-end data analytics capstone project built on the **Microsoft Fabric** ecosystem, covering everything from data ingestion and engineering to warehousing and interactive Power BI visualization. This project simulates a real-world business intelligence pipeline for analyzing Swiggy food order data.

---

## 📌 Project Objective

The primary goal of this project is to build a complete, production-style data pipeline and analytics solution. Specifically, the project aims to:

- Ingest and store raw Swiggy order data in a unified data platform.
- Process and clean the data using SQL and Data Factory pipelines.
- Model the data into a **Star Schema** within a Data Warehouse.
- Deliver actionable business insights through a dynamic, interactive **Power BI dashboard**.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **Microsoft Fabric** | Core unified platform for data engineering, warehousing, and analytics |
| **OneLake** | Unified storage layer ("OneDrive for data") for all organizational data |
| **Data Factory (Pipelines)** | Orchestrates data movement from Lakehouse to Data Warehouse |
| **SQL (T-SQL)** | Data validation, cleaning (nulls/duplicates), and querying the SQL analytics endpoint |
| **Power BI** | Semantic modeling and interactive visualization layer |
| **Python (Jupyter Notebook)** | Local exploratory data analysis (EDA) and SQL query testing/validation, using imported data outside the Fabric pipeline |
| **Azure Data Lake Storage (ADLS) Gen2** | Underlying storage engine for the Lakehouse and Warehouse |

---

## 🏗️ Architecture & Workflow

This project follows the **Medallion Architecture** pattern (Bronze → Silver → Gold):

1. **Bronze Layer (Lakehouse)**
   Raw CSV data is uploaded to the Lakehouse `Files` section and converted into Parquet/Delta tables.

2. **Silver/Gold Layer (Data Warehouse)**
   Data is moved from the Lakehouse to a Data Warehouse using Data Factory pipelines.

3. **Data Transformation**
   T-SQL is used to clean and structure the data — including creating a primary key (`order_id`) and converting string-based dates into proper date formats using the `TRY_CONVERT` function.

4. **Semantic Modeling**
   A **Star Schema** is designed by connecting a central **Fact table (Orders)** to multiple **Dimension tables** (Date, Dish, Location, Restaurant) via one-to-many relationships.

5. **Visualization**
   A Power BI report is built using **DirectLake** (or DirectQuery mode for local development), then published back to the Fabric workspace.

```
Raw CSV → Lakehouse (Bronze) → Data Factory Pipeline → Data Warehouse (Silver/Gold)
        → T-SQL Cleaning & Transformation → Star Schema → Power BI (DirectLake) → Published Report
```

---

## 📊 Key Analysis Features

### KPIs Monitored
- **Total Sales** — Overall revenue generated from food orders.
- **Average Rating** — Customer satisfaction levels across all restaurants.
- **Average Order Value (AOV)** — Revenue generated per single order.
- **Total Orders & Rating Count** — Volume of orders and total customer reviews.

### Visualizations Included
- 📈 Monthly, Weekly, and Daily Sales Trends — identifying peak periods and fluctuations.
- 🥗 Total Sales by Food Type (Veg vs. Non-Veg) using calculated columns.
- 🗺️ Sales by State/City — geographic performance analysis using maps and bar charts.
- 🏆 Top 5 Restaurants — identifying high-performing restaurant partners.

---

## 🗃️ Data Overview

The dataset contains approximately **197,430 rows** of Swiggy order data covering **January – August 2025**.

**Dimensions:**
- State
- City
- Order Date
- Restaurant Name
- Location
- Category
- Dish Name

**Facts:**
- Price
- Rating
- Rating Count

---

## 📝 Notes on Tooling

While the core pipeline (ingestion, transformation, warehousing, and visualization) was built entirely within Microsoft Fabric, two supplementary **Jupyter Notebooks** were used locally (outside Fabric, with imported data) for:
- **Exploratory Data Analysis (EDA)** — checking data distributions, nulls, and general data quality before pipeline design.
- **SQL Query Testing** — validating and iterating on query logic prior to running it against the Fabric SQL analytics endpoint.

These notebooks were used as a local development aid and are not part of the production pipeline.

---

## 📂 Project Structure

```
swiggy-sales-analysis/
├── data/                  # Raw CSV source data
├── notebooks/
│   ├── eda.ipynb          # Local exploratory data analysis (Jupyter)
│   └── sql_testing.ipynb  # Local SQL query testing/validation (Jupyter)
├── pipelines/
│   ├── Pipeline_load_data_from_files_to_tables.json  # Bronze: CSV → Lakehouse Delta tables
│   ├── pipeline_lw_to_dw.json                         # Silver/Gold: Lakehouse → Data Warehouse
│   └── README.md                                      # Explanation of each pipeline
├── powerbi/               # Power BI report (.pbix) and semantic model
├── docs/                  # Architecture diagrams & documentation
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- A Microsoft Fabric-enabled workspace (Fabric trial or licensed capacity)
- Power BI Desktop (for local report development)
- Access to OneLake / Lakehouse and Data Warehouse within your workspace

### Steps
1. Create a Fabric workspace and enable Fabric capacity.
2. Create a **Lakehouse** and upload the raw Swiggy CSV data to the `Files` section.
3. Convert the raw files into Delta tables (Bronze layer).
4. Build a **Data Factory pipeline** to move data into the **Data Warehouse**.
5. Run the provided T-SQL scripts to clean data and create the primary key and formatted date columns.
6. Build the **Star Schema** by defining relationships between the Fact and Dimension tables.
7. Connect **Power BI Desktop** to the Warehouse via DirectQuery, build the report, and publish it to the Fabric workspace using DirectLake.

---

## 📈 Sample Insights

- Identification of peak ordering days/times across the dataset period.
- Comparison of Veg vs. Non-Veg order revenue contribution.
- State- and city-level performance heatmaps.
- Ranking of top restaurant partners by sales volume and revenue.

---
## 📸 Dashboard Preview

![Power BI Dashboard](https://github.com/Abhi20703/-Swiggy-Sales-Dashboard-An-End-to-End-Microsoft-Fabric-Pipeline/blob/main/power%20bi/Swiggy%20Dashboard.png)

*Interactive Power BI dashboard showing sales trends, KPIs, and geographic performance.*
---

## 📜 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

