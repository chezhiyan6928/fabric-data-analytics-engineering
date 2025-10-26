# Financial Analytics Project (Fabric + Power BI)

### Goal:
Build a sales analytics pipeline using Microsoft Fabric Lakehouse and PySpark.

### Steps:
1. **Bronze:** Ingest Excel/CSV data → Lakehouse.
2. **Silver:** Clean columns (remove `$`, handle nulls, cast datatypes).
3. **Gold:** Aggregate metrics (country, segment, product).
4. Visualize KPIs in Power BI.

**Highlights:**
- Profit Margin %, Monthly & Quarterly trends
- Filters: Country / Product / Segment
- Delta tables for reliable data layers
