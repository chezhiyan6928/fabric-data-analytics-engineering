# 📈 Real-Time Stock Market Data Pipeline (Microsoft Fabric)

## Project Overview
This project implements an end-to-end **Data Engineering pipeline** on **Microsoft Fabric**, designed to ingest, process, and visualize stock market data daily. It demonstrates a modern **Lakehouse architecture** using **Medallion principles** (Bronze $\rightarrow$ Silver $\rightarrow$ Gold).

The system automatically fetches daily data for major tech stocks (AAPL, MSFT, GOOGL, AMZN), calculates technical indicators (7-Day SMA) using **PySpark**, and updates a dimensional model for low-latency reporting.

---

## 🏗️ Architecture & Technology Stack

* **Cloud Platform:** Microsoft Fabric (OneLake, Lakehouse)
* **Orchestration:** Fabric Data Pipeline (Daily Scheduled Run)
* **Compute:** Spark Pool (PySpark Notebooks)
* **Storage Format:** Delta Lake (Parquet with ACID compliance)
* **Visualization:** Power BI (Direct Lake mode)

### Data Flow
1.  **Extraction (Bronze):** Python script fetches raw data from Yahoo Finance API via `yfinance` library.
2.  **Transformation (Silver):**
    * Data cleansing and type casting.
    * **Complex Transformation:** Calculating 7-day Simple Moving Average (SMA) using **Spark Window Functions**.
3.  **Load (Gold):**
    * **Incremental Loading:** Using Delta Lake `MERGE` (Upsert) to efficiently update history with new daily records.
    * **Optimization:** Gold table partitioned by `Year` and `Ticker` for fast query performance.
4.  **Serving:** Power BI connects directly to Gold tables via Direct Lake.

---

## 🚀 Key Engineering Highlights (DP-700 Skills)

* **Incremental Data Processing:** Implemented a robust **Delta MERGE** strategy to handle daily upserts without full table reloads, optimizing compute costs.
* **Advanced PySpark Transformations:** Utilized Window functions for time-series analytics (`avg(close).over(window_spec)`).
* **Schema Enforcement:** Used `.option("overwriteSchema", "true")` and explicit casting to manage schema evolution between Pandas and Spark.
* **Automated Orchestration:** Built a scheduled Data Pipeline that handles library dependencies (`%pip install`) and executes the daily update notebook.
* **Dimensional Modeling:** Created a Star Schema with `FactStocks` (Gold) and `DimCompany`/`DimDate` for robust reporting.

---

## 📊 Final Dashboard

*(Insert your Power BI screenshot here showing the Price vs. SMA chart)*

The final dashboard allows analysts to compare daily price movements against the 7-day moving average trendline for any selected stock.

---

## 📂 Repository Structure

* **`notebooks/`**: Contains the PySpark code for historical backfill and daily incremental updates.

* graph LR
    %% Styles
    classDef source fill:#f9f9f9,stroke:#333,stroke-width:2px;
    classDef fabric fill:#dbf3ff,stroke:#0078d4,stroke-width:2px,stroke-dasharray: 5 5;
    classDef storage fill:#ffe0b2,stroke:#f57c00,stroke-width:2px;
    classDef process fill:#c8e6c9,stroke:#388e3c,stroke-width:2px;
    classDef serving fill:#e1bee7,stroke:#8e24aa,stroke-width:2px;

    %% External Source
    subgraph Source [External Data Source]
        API[Yahoo Finance API]:::source
    end

    %% Microsoft Fabric Environment
    subgraph Fabric [Microsoft Fabric Workspace]
        direction TB
        
        %% Orchestration
        Pipeline[Fabric Data Pipeline<br/>(Daily Schedule)]:::process

        %% Notebooks / Processing
        NB_Daily[NB_02: Daily Incremental<br/>(PySpark/Python)]:::process

        %% Storage Layers (OneLake)
        subgraph OneLake [OneLake Storage]
            direction LR
            Bronze[(Bronze Layer<br/>Raw Delta Files)]:::storage
            Silver[(Silver Layer<br/>Cleaned Delta Table)]:::storage
            Gold[(Gold Layer<br/>Partitioned Delta Table)]:::storage
        end

        %% Visualization
        PBI[Power BI Dashboard<br/>(Direct Lake Mode)]:::serving
    end

    %% Flows
    API -->|"Extract (Python/yfinance)"| NB_Daily
    Pipeline -->|"Triggers (Daily @ 6AM)"| NB_Daily
    NB_Daily -->|"Load New Data"| Bronze
    Bronze -->|"Read Raw"| NB_Daily
    NB_Daily -->|"Transform & MERGE (Upsert)"| Silver
    Silver -->|"Read Updated History"| NB_Daily
    NB_Daily -->|"Optimize & Partition"| Gold
    Gold -->|"Direct Lake Query"| PBI

    %% Styling links
    linkStyle default stroke-width:2px,fill:none,stroke:gray;
