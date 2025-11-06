graph LR
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
