# Downscaling SMAP Soil Moisture over Sri Lanka using Deep Learning and Multi-Source Remote Sensing
## Overview
Soil moisture is a critical variable for understanding droughts, agricultural productivity, and land–atmosphere interactions. However, satellite-derived soil moisture products such as SMAP are available at relatively coarse spatial resolutions (~9–10 km), limiting their applicability for local-scale hydrological and agricultural studies.

This project presents a deep learning–based spatial downscaling framework to estimate 1 km soil moisture by learning the relationship between SMAP soil moisture and multi-source Earth Observation (EO) variables. The model is trained at 10 km resolution and subsequently applied at 1 km resolution using higher-resolution predictor variables.

The analysis is applied to a custom Region of Interest (ROI) covering parts of the North Central Province and Northern Province of Sri Lanka, regions that are climatically sensitive and highly dependent on soil moisture availability for agriculture and water resource management.

### Figure 1. Original SMAP Soil Moisture (10 km) - Monthly SMAP surface soil moisture at ~10 km spatial resolution for 2020 over parts of the North Central and Northern Provinces of Sri Lanka, showing broad-scale moisture patterns captured by the native SMAP product.
<img width="1686" height="590" alt="image" src="https://github.com/user-attachments/assets/5e2db570-05f8-4623-bd8e-8da6f72f78b0" />

### Figure 2. Downscaled Soil Moisture (1 km) - Neural network–downscaled soil moisture at 1 km spatial resolution for 2020, generated using MODIS vegetation indices, land surface temperature, evapotranspiration, elevation, and land cover, providing enhanced spatial detail compared to the original SMAP product.
<img width="1687" height="590" alt="image" src="https://github.com/user-attachments/assets/47b8dc59-2521-48f3-8df7-ad310fc12767" />


## Study Area
- Location: Northern and North Central Provinces, Sri Lanka
- ROI Definition: User-defined polygon drawn interactively in geemap
- Characteristics:
    1. Semi-arid to dry-zone climate
    2. Strong seasonal variability
    3. High dependence on rain-fed and irrigated agriculture

## Data Sources
- All datasets are accessed via Google Earth Engine (GEE).
1. Target Variable
- SMAP Soil Moisture
a. Dataset: NASA/SMAP/SPL3SMP_E/005
b. Variable: soil_moisture_am
c. Native Resolution: ~9–10 km
d. Temporal Aggregation: Monthly mean (2016–2024)
e. Role: Prediction target (training at 10 km)

2. Predictor Variables

| Variable           | Dataset         | Native Resolution | Purpose                 |
| ------------------ | --------------- | ----------------- | ----------------------- |
| NDVI, EVI          | MODIS MOD13Q1   | 250 m             | Vegetation condition    |
| Day LST            | MODIS MOD11A2   | 1 km              | Surface temperature     |
| Night LST          | MODIS MOD11A2   | 1 km              | Thermal inertia         |
| Evapotranspiration | MODIS MOD16A2GF | 500 m             | Surface water loss      |
| Elevation          | USGS GTOPO30    | ~1 km             | Topographic control     |
| Land Cover         | MODIS MCD12Q1   | 500 m             | Surface characteristics |

All predictors are:
1. Aggregated to monthly means
2. Resampled internally by GEE to match the requested scale

## Tools & Libraries
1. Google Earth Engine (GEE) – data access and preprocessing
2. geemap – interactive mapping and ROI selection
3. xee – GEE–xarray integration
4. xarray – spatiotemporal data handling
5. NumPy / Pandas – data processing
6. scikit-learn – scaling, train-test split, evaluation
7. TensorFlow / Keras – deep learning model
8. Matplotlib – visualization

## Notes & Assumptions
- The model assumes stationarity of the SM–EO relationship across scales.
- Elevation and land cover act as static spatial constraints.
- Downscaled soil moisture represents relative spatial variability, not in-situ truth.
- Results are best suited for:
    1. Drought monitoring
    2. Agricultural analysis
    3. Hydrological modelling support
- Ground validation is recommended for operational use.
