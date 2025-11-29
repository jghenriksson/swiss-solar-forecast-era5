# Swiss Solar Forecast (ERA5 & Deep Learning)

This project implements an end-to-end pipeline for forecasting hourly solar PV generation in Switzerland using ERA5 climate reanalysis data and deep learning models. It integrates multiple data sources, performs extensive feature engineering, and prepares spatiotemporal sequences for LSTM-based forecasting.

## Overview

This project covers the full workflow of building a data-driven solar forecasting model:

- Downloading and processing ERA5 atmospheric variables (temperature, radiation, wind, cloud cover, etc.)
- Population-weighted spatial aggregation using WorldPop data  
- Solar geometry feature engineering (cosine of solar zenith angle, sun vector components)
- Heuristic snow cover modelling to represent PV system obstructions in winter
- PV generation modelling using ENTSO-E historical data
- Capacity-normalisation using Ember Climate solar capacity statistics
- Spatiotemporal sequence preparation for deep learning models (LSTM)

The project is designed to be modular and reproducible, with a clear separation between data acquisition, feature engineering, and model training.

<img width="1577" height="478" alt="image" src="https://github.com/user-attachments/assets/66976286-7f9b-4e7e-a407-059ea60782b5" />

## Data Sources

This project integrates multiple public data sources:

- **ERA5 reanalysis weather data** (Copernicus Climate Data Store)  
  Used for hourly meteorological variables such as temperature, cloud cover, wind, radiation, humidity, precipitation, and boundary layer properties.

- **ENTSO-E Transparency Platform**  
  Used for historical national solar PV generation time series.

- **WorldPop (worldpop.org)**  
  Used for population density data, enabling population-weighted spatial aggregation of meteorological features.

- **Ember Climate**  
  Used for national-level historical solar capacity data, enabling capacity-normalised feature engineering.

All datasets are processed and aligned to a common hourly UTC timeline.

## Features

Key engineered features used in the model include:

- **Population-weighted ERA5 variables** (temperature, cloud cover, wind, radiation, humidity, precipitation, boundary layer height…)
- **Solar geometry**  
  - cosine of solar zenith angle (`cos_sza` / `mu0`)  
  - sun vector components (`sun_x`, `sun_y`, `sun_z`)
- **Clear-sky irradiance** using a fast Haurwitz model
- **Clear-sky index (`kstar`)**  
- **Heuristic snow state model** representing accumulated snowfall, melting, and wind shedding
- **Wind direction decomposition** into `wind_dir_x` and `wind_dir_y`
- **Capacity scaling** using monthly solar capacity factors from Ember

- ## Installation

Clone the repository and install dependencies:
```bash
git clone https://github.com/jghenriksson/solar-pv-forecasting-era5.git
cd solar-pv-forecasting-era5
pip install -r requirements.txt
```

## Notes

- ERA5 data must be downloaded via the CDS API. You will need a CDS account and API key.
- Large NetCDF files are not included in this repository. They must be downloaded locally.
- The project assumes data is processed in UTC time.
- TensorFlow 2.20.0 was used for model development.

## Future Work

Potential extensions of this project include:

- Transformer-based temporal models
- Probabilistic forecasting with uncertainty estimation
- Intraday satellite-based cloud nowcasting integration
- Spatial CNN encoder for full-gridded ERA5 fields
