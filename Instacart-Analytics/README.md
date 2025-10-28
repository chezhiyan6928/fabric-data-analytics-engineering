# 🛒 Microsoft Fabric Analytics: Instacart E-commerce Pipeline

This project demonstrates expertise in **Data Analytics Engineering** by designing, building, and deploying a scalable Star Schema data model using the **Microsoft Fabric** platform, from raw ingestion to dashboard delivery. The solution processes over **32 million transactional records** from the Instacart Open Dataset to derive critical retail KPIs.

---

## 🛠️ Technology Stack

* **Cloud Platform:** Microsoft Fabric (OneLake, Lakehouse)
* **Data Engineering (DP-700 Focus):** PySpark (Notebooks), Dataflow Gen2 (Power Query M), Delta Lake
* **Data Modeling (DP-600 Focus):** Star Schema, DAX (Data Analysis Expressions), Semantic Model
* **Visualization:** Power BI (Direct Lake connectivity)

---

## 💡 Key Deliverables & Engineering Focus

### 1. Robust Data Pipeline Architecture
* **Hybrid ELT:** Designed a pipeline utilizing **Dataflow Gen2** for cleansing and modeling dimension tables (`DimProduct`, `DimAisle`) and **PySpark** for complex joins on high-volume transactional data.
* **Data Quality & Integrity:** Enforced schema consistency and data quality checks (e.g., null-to-zero handling for first-time orders, explicit type casting) before loading into the Silver/Gold layers.

### 2. Star Schema & Semantic Modeling
* **Dimensional Modeling:** Built a canonical Star Schema centered around the **`FactOrders`** table, linked to time and product dimensions.
* **DAX Governance:** Developed core **analytical measures** (e.g., `Products Per Order`, `Total Orders`) within the Semantic Model, ensuring data is ready for consumption by business stakeholders.
* **Time Attribute Handling:** Created a separate **DAX Day Dimension Table (`DimDay`)** and sorting logic to ensure correct sequencing and labeling of sales data.

### 3. Final Analytical Output
* **High-Performance Dashboard:** Delivered a professional Power BI report using **Direct Lake** mode for low-latency queries.
* **Actionable Insights:** Visualized key retail metrics, including: **Peak Hourly Demand** (for logistics staffing), **Daily Sales Trends**, and the **Average Basket Size** (`Products Per Order`).

---

## 📊 Project Visuals

<img width="1358" height="753" alt="image" src="https://github.com/user-attachments/assets/8523a509-465e-436b-a6bc-54524ff631eb" />



---

## 📂 Repository Contents

* `notebooks/Instacart_Fact_Transform.ipynb`: PySpark code for Fact table creation and cleaning.
* `reports/Instacart_Dashboard.pbix`: Final Power BI report file.
* `data/`: (Placeholder for raw data files/link to source)
