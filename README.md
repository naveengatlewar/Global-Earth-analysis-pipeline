# 🌍 End-to-End Data Engineering Project: Global Earthquake Analysis

![Microsoft Fabric](https://img.shields.io/badge/Microsoft%20Fabric-Enabled-blue) ![Status](https://img.shields.io/badge/Status-Completed-success) ![Power BI](https://img.shields.io/badge/Power%20BI-Direct%20Lake-yellow)

## 📋 Project Overview
This project demonstrates a full-scale **Data Engineering** solution built entirely within the **Microsoft Fabric** ecosystem. The goal was to build an automated ETL pipeline that ingests real-time earthquake data, processes it through a multi-hop architecture, and visualizes it for geospatial analysis.

The system is designed to handle **incremental daily loads**, ensuring the dashboard always reflects the most recent 24 hours of global seismic activity without manual intervention.

## 🏗️ Architecture
The project follows the **Medallion Architecture** (Lakehouse Design Pattern):

1.  **Bronze Layer (Raw):** Ingests raw JSON data from the USGS API via Python scripts.
2.  **Silver Layer (Cleaned):** Flattens nested JSON structures, handles timestamp conversions (Unix to DateTime), and deduplicates data using **PySpark**.
3.  **Gold Layer (Enriched):** Enriches earthquake data with geolocation details (Country Codes) using `reverse_geocoder` and classifies events by significance (Low/Moderate/High).

## 🛠️ Tech Stack
* **Platform:** Microsoft Fabric
* **Orchestration:** Data Factory (Pipelines)
* **Compute/Processing:** Synapse Data Engineering (Notebooks, Spark Pools)
* **Language:** Python (PySpark, Pandas)
* **Storage:** OneLake (Delta Tables)
* **Visualization:** Power BI (Direct Lake Mode)

## 🚀 Key Features
* **Automated Data Ingestion:** A Data Factory pipeline triggers daily to fetch data from the [USGS Earthquake API](https://earthquake.usgs.gov/fdsnws/event/1/).
* **Dynamic Parameterization:** Utilized Data Factory expressions (`@addDays`, `@utcNow`) to dynamically pass date ranges to notebooks, enabling efficient incremental loading.
* **Geospatial Enrichment:** Integrated external Python libraries to map latitude/longitude coordinates to specific country ISO codes for better reporting.
* **Direct Lake Reporting:** Power BI connects directly to Delta Tables in OneLake, bypassing the need for import refreshes and enabling high-performance querying.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect_with_Me-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/posts/naveen-g-071613147_dataengineering-microsoftfabric-dp700-activity-7422184414652227584-b6qV?utm_source=share&utm_medium=member_desktop&rcm=ACoAACOCHZUBg3T82oYS0Y_WtneNbJ_xYZO0-fg)

## 📂 Repository Structure
```bash
├── Notebooks/
│   ├── 01_Bronze_Ingestion.ipynb   # Fetches API data -> JSON
│   ├── 02_Silver_Transformation.ipynb # Flattens JSON -> Delta Table
│   └── 03_Gold_Enrichment.ipynb    # Adds Country Codes -> Gold Delta Table
└── README.md
