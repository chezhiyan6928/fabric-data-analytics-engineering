# Microsoft Fabric — Data Engineering Portfolio

**Author:** Dhananchezhiyan  
**Role:** QA Engineer (BI & ETL Tester) | Aspiring Data Engineer & Analytics Specialist

---

## 📘 Overview
This repository showcases **end-to-end Data Engineering & Analytics projects** built on **Microsoft Fabric** using **PySpark**, **Dataflows**, and **Power BI**.  
Each project follows the **Medallion Architecture** (Bronze → Silver → Gold) for structured data transformation, storage, and analysis.

Projects included:
- **Financial Analytics Project** — A structured ETL pipeline that cleans and aggregates sales & profit data.
- **Earthquake Analytics Project** — A real-world Fabric + PySpark pipeline using USGS data and reverse geocoding enrichment.

---
---

## 🧩 Technologies Used
- **Microsoft Fabric Lakehouse**
- **PySpark (Spark SQL, DataFrame API)**
- **Power BI (Dashboard Visualization)**
- **Delta Lake Format**
- **Python (UDFs, API Ingestion, Data Cleaning)**

---

## 🚀 Financial Analytics Project
**Objective:**  
Transform raw sales data (with currency symbols, nulls, inconsistent formats) into an analytical gold table showing:
- Yearly / Quarterly / Monthly trends  
- Country-, Segment-, and Product-level Profit & Sales  
- Profit Margin % computation  

**Key Highlights:**
- Cleaned and casted financial data using PySpark.
- Removed `$` symbols using `regexp_replace`.
- Derived `profit_margin_percentage = (profit / sales) * 100`.
- Published professional Power BI dashboard with filters and date hierarchy.

📄 [View Dashboard (PDF)](Financial_Analytics/report/financial_dashboard.pdf)

---

## 🌎 Earthquake Analytics Project
**Objective:**  
Ingest and process real-world earthquake data using USGS API → enrich with geolocation & significance classification → prepare for Power BI visualization.

**Key Highlights:**
- API ingestion using Python `requests`.
- Flattened nested JSON (geometry + properties fields).
- Enriched with reverse geocoding (country mapping).
- Classified significance levels (`Low`, `Moderate`, `High`).
- Stored in Delta Gold table for visualization.

📄 [View Dashboard (PDF)](Earthquakes_Analytics/Earthquake_Event.pdf)

---

## 🧠 Concepts Demonstrated
✅ Medallion Architecture (Bronze / Silver / Gold)  
✅ Delta Tables & Schema Handling (`mergeSchema`, `overwriteSchema`)  
✅ PySpark Transformations (`withColumn`, `cast`, `groupBy`)  
✅ Aggregations & Derived Metrics  
✅ Power BI Integration with Fabric Lakehouse  

---
