# Earthquake Analytics Project (Fabric + PySpark)

### Goal:
Ingest and enrich real-world earthquake data from USGS API.

### Steps:
1. **Bronze:** Fetch and store GeoJSON from USGS API.
2. **Silver:** Flatten structure (coordinates, properties).
3. **Gold:** Add country info via reverse geocoding and classify events by significance.

**Highlights:**
- Used PySpark UDFs for geocoding.
- Created Gold table for country-wise earthquake significance.
- Power BI visualizations for severity and region analysis.
