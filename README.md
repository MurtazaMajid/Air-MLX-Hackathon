# Parking Violation Risk Prediction
### Air University MLX Hackathon 2025 — 1st Place · RMSE: 0.13

![Winner](https://img.shields.io/badge/Air_MLX_2025-1st_Place-ffb86c?style=for-the-badge&labelColor=0d0d0d)
![RMSE](https://img.shields.io/badge/Winning_RMSE-0.13-50fa7b?style=for-the-badge&labelColor=0d0d0d)
![Stack](https://img.shields.io/badge/Stack-Python_·_Pandas_·_Sklearn-bd93f9?style=for-the-badge&labelColor=0d0d0d)

---

## The Challenge

A one-day hackathon hosted by Air University, Islamabad as part of MLX 2025. The task was to predict `invalid_ratio`, the proportion of invalid parking events at a given location and time, using data spread across five relational SQLite tables.

A `.db` file, a baseline to beat, and 2 hours to do it.

---

## The Data

Five tables, one database, no documentation:

| Table | Contents |
|---|---|
| `participants` | Sensor and participant identifiers |
| `weather_info` | Temperature, humidity, weather alerts |
| `location_info` | Parking zone data |
| `timestamps` | Hour, day, month |
| `measurements` | Sensor readings and the target label |

The target column `invalid_ratio` was stored as a plain string like `"0.23 (23%)"` and had to be parsed with regex before any modelling could start.

---

## What Was Done

```
Five SQLite tables extracted and merged into one flat DataFrame
Target column parsed from string to float using regex
Zero-variance column dropped (snow_possible)
Categorical columns one-hot encoded (weather_alert, day_period)
Missing values filled with mean or mode depending on column type
Sensor columns z-score normalised
Three model variants compared:
  Linear Regression on raw features
  Linear Regression on normalised features
  Linear Regression with PCA (95% variance retained)
Winning RMSE: 0.13
```

---

## Results

| Model | RMSE |
|---|---|
| Linear Regression, raw | baseline |
| Linear Regression, normalised | improved |
| **Linear Regression with PCA** | **0.13** |

Reducing the noisy sensor columns with PCA while retaining 95% of variance gave the best result.

---

## Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

---

## What Worked

The data engineering was the hard part, not the model. The target was a string, the data was split across five tables, and there were nulls everywhere. Getting that right under time pressure was what won it.

PCA on the unnamed sensor columns outperformed both the raw and normalised baselines. No ensembles, no tuning. Clean data and the right preprocessing was enough.

---

<div align="center">
  <sub>Built in a few hours · Air MLX Hackathon 2025 · Air University, Islamabad</sub>
</div>
