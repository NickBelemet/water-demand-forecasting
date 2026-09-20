# Data

The original dataset used in this project is **not included in this
repository** because it contains proprietary operational data supplied
for academic research purposes.

## Dataset Overview

The study used Distribution Input (DI) data from eight Water Treatment
Works (WTWs) in the South West Water network during 2024.

The original time-series dataset contained **35,138 timestamped
observations at 15-minute intervals**. The modelling experiments in
this repository focus primarily on **Restormel Water Treatment Works**
as a case study.

Distribution Input represents the volume of treated water entering the
water supply network and forms an important operational measure for
water utilities.

## Features

The modelling pipeline derived temporal features including:

- Hour of day
- Day of week
- Month of year
- Weekend indicator
- Cyclical sine/cosine encodings

The high-frequency DI observations were also resampled where appropriate
for the forecasting experiments.

## Data Availability

Due to data-sharing restrictions, the raw and processed datasets cannot
be redistributed publicly.

The notebooks are provided to demonstrate the preprocessing,
feature-engineering, modelling and evaluation methodology used in the
research.
