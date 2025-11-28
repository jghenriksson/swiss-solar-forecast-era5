# Solar PV Forecasting with ERA5

This project implements an end-to-end pipeline for short-term solar photovoltaic (PV) power forecasting using ERA5 reanalysis weather data.  
It combines physically inspired feature engineering with deep learning models to predict solar power generation from meteorological drivers.

## Overview

The workflow in this project includes:

- Downloading and processing ERA5 reanalysis data from the Copernicus Climate Data Store
- Population-weighted spatial aggregation of meteorological variables
- Solar geometry feature engineering (solar zenith and sun vector components)
- Heuristic snow cover modelling to capture seasonal panel obstruction effects
- Preparation of spatiotemporal input sequences
- Deep learning–based forecasting using LSTM architectures

The project is designed to be modular and reproducible, with a clear separation between data acquisition, feature engineering, and model training.


## Data Sources

This project integrates multiple public data sources:

- **ERA5 reanalysis weather data** (Copernicus Climate Data Store)  
  Used for hourly meteorological variables such as temperature, cloud cover, wind, radiation, humidity, precipitation, and boundary layer properties.

- **ENTSO-E Transparency Platform**  
  Used for historical national and regional solar PV generation time series.

- **WorldPop (worldpop.org)**  
  Used for population density data, enabling population-weighted spatial aggregation of meteorological features.

- **Ember Climate**  
  Used for national-level historical and projected solar capacity data, enabling capacity-normalised feature engineering.

All datasets are processed and aligned to a common hourly UTC timeline.

## Features

Key engineered features used in the model include:

- Population-weighted meteorological variables
- Solar zenith and sun position vectors  
- Clear-sky radiation approximations
- Snow cover state modelling
- Wind speed and direction components
- Boundary layer and cloud structure variables

- ## Installation

Clone the repository and install dependencies:

git clone https://github.com/jghenriksson/solar-pv-forecasting-era5.git
cd solar-pv-forecasting-era5
pip install -r requirements.txt


## Notes

ERA5 data must be downloaded via the CDS API. You will need a CDS account and API key.

The project assumes data is processed in UTC time.

Large NetCDF/GRIB files are not stored in the repository and must be downloaded locally.

## Future Work

Potential extensions of this project include:

- Transformer-based temporal models
- Probabilistic forecasting with uncertainty estimation
- Intraday satellite-based cloud nowcasting integration
