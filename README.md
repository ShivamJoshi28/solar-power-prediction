
# Solar Power Output Prediction

## Overview
This project tries to predict the total generation of AC_POWER through features like location-temperature, module-temperature, hour of day, month of year and irradiation. I have tried 3 algorithems- Linear regression, RandomForest and XGBoost, and from that i have concluded that XGBoost performs best with the lowest RMSE of 46.87 and R² of 0.9858

## Dataset
- Source: Kaggle — Solar Power Generation Data by anikannal
- Two files merged: generation data (68,778 rows) and weather sensor data
- Plant location: India (Plant ID 4135001)

## Features used
- AMBIENT_TEMPERATURE, MODULE_TEMPERATURE, IRRADIATION
- hour, month (extracted from timestamp)

## Models and results
| Model | RMSE | R² |
|-------|------|----|
| Linear Regression | 56.71 | 0.9792 |
| Random Forest | 46.94 | 0.9857 |
| XGBoost | 46.87 | 0.9858 |

## Key finding
Irradiation is almost the only thing that matters, with everything else barely registering. it's reasonable because irradiation is the amount of solar energy hitting the panels — it's the direct input to power generation. Temperature, hour, and month are all just indirect proxies for the same thing. When you have the actual irradiation reading, those other features add almost nothing.

## Data leakage note
I excluded DC_POWER and DAILY_YIELD because AC_POWER is converted using DC_POWER and DAILY_YIELD is calculated using AC_POWER. SO taking them into account was causing data leakage, meaning that while precision was 100%, the model was actaully learning nothing. As DC_POWER and AC_POWER will be recorded on the same time and DAILY_YIELD will be recorded after AC_POWER.

## How to run
1. Download Plant_1_Generation_Data.csv and Plant_1_Weather_Sensor_Data.csv from Kaggle or from this repo.
2. Upload both to Google Colab
3. Open solar_power_project_2.ipynb and run all cells

## Libraries used
pandas, scikit-learn, xgboost, matplotlib
