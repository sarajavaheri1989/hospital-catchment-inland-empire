# Hospital Catchment Area Analytics in the Inland Empire

A reproducible geospatial data pipeline for healthcare accessibility analysis in California's Inland Empire (Riverside County and San Bernardino County).

**Author:** Sara Javaheri, Graduate Research Assistant, California State University, San Bernardino
**Faculty Mentor:** Dr. Benjamin J. Becerra, Assistant Professor, School of Cyber and Decision Sciences

## Overview

This notebook documents the complete data engineering workflow used to build an integrated geospatial database for hospital catchment area and healthcare accessibility research. It combines census tract boundaries, demographic and socioeconomic data, public health indicators, hospital and health center locations, and road network data into a single analytical layer, with validation performed at every integration step.

This workflow supports a broader research project examining disparities in healthcare access to high blood pressure and diabetes care across the Inland Empire, presented at CSUSB's Meeting of the Minds symposium.

## What this notebook does

1. Prepares official U.S. Census Bureau TIGER/Line census tract boundaries for the study area
2. Retrieves tract-level demographic data from the American Community Survey (ACS) via the Census API
3. Integrates CDC PLACES tract-level chronic disease prevalence estimates
4. Filters and geocodes CMS hospital location data
5. Filters and validates HRSA health center location data
6. Prepares OpenStreetMap road network data for future drive-time accessibility modeling
7. Validates every join and spatial integration step (match rates, coordinate reference systems, missing-data checks)

## Data sources

All data used in this project is public. Raw data files are not included in this repository — download links and citations are provided below so the pipeline can be reproduced.

| Dataset | Publisher | Source | Download | License |
|---|---|---|---|---|
| TIGER/Line Census Tracts 2025 (California) | U.S. Census Bureau | [Source page](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html) | [Download](https://www2.census.gov/geo/tiger/TIGER2025/TRACT/tl_2025_06_tract.zip) | Public domain (U.S. Government) |
| ACS 5-Year Demographics (2020–2024) | U.S. Census Bureau | [Census API](https://api.census.gov/data/2024/acs/acs5) | Retrieved via Census API (requires a free API key) | Public U.S. government data |
| CDC PLACES Census Tract Data (GIS-Friendly Format), 2024 release | Centers for Disease Control and Prevention | [Source page](https://data.cdc.gov/500-Cities-Places/PLACES-Census-Tract-Data-GIS-Friendly-Format-2022-/shc3-fzig) | [Download](https://data.cdc.gov/resource/shc3-fzig.csv?$limit=200000) | Public; CDC open data terms |
| CMS Hospital General Information | Centers for Medicare & Medicaid Services | [Source page](https://data.cms.gov/provider-data/dataset/xubh-q36u) | [Download](https://data.cms.gov/provider-data/api/1/datastore/query/xubh-q36u/0/download?format=csv) | Public; CMS terms |
| HRSA Health Center Service Delivery and Look-Alike Sites | Health Resources and Services Administration | [Source page](https://data.hrsa.gov/topics/health-centers) | [Download](https://data.hrsa.gov/DataDownload/DD_Files/Health_Center_Service_Delivery_and_LookAlike_Sites.csv) | Public; HRSA terms |
| OpenStreetMap Roads – Southern California | OpenStreetMap contributors, via Geofabrik GmbH | [Source page](https://download.geofabrik.de/north-america/us/california/socal.html) | [Shapefile download](https://download.geofabrik.de/north-america/us/california/socal-latest-free.shp.zip) | Open Database License (ODbL) 1.0 |

### Citations

- U.S. Census Bureau. (2025). *TIGER/Line Shapefiles*.
- U.S. Census Bureau. (2024). *American Community Survey 5-Year Estimates*, accessed via Census API.
- Centers for Disease Control and Prevention. (n.d.). *PLACES Census Tract Data (GIS-friendly format)*.
- Centers for Medicare & Medicaid Services. (n.d.). *Hospital General Information*.
- Health Resources and Services Administration. (n.d.). *Health Center Service Delivery and Look-Alike Sites*.
- OpenStreetMap contributors; Geofabrik GmbH. (2026). *OpenStreetMap road network data, Southern California*.

## How to run this notebook

1. Clone this repository
2. Install dependencies: `geopandas`, `pandas`, `census`, `geopy`, `matplotlib`, `shapely`
3. Request a free U.S. Census Bureau API key at [api.census.gov](https://api.census.gov/data/key_signup.html) and set it as an environment variable:
   ```bash
   export CENSUS_API_KEY="your_key_here"
   ```
4. Download the datasets listed above into a local `data/raw/` folder
5. Run the notebook cells in order

## Acknowledgements

This work was developed as part of an ongoing research project in Dr. Benjamin J. Becerra's research group at CSUSB, with contributions from Ryan Strong, Jackson Bowden, Rong Cong, and Alexander Griessbach.
