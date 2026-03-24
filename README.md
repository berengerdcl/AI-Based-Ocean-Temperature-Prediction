# AI-Based Ocean Temperature Prediction

## Overview
End-to-end machine learning pipeline predicting ocean temperature from 
real oceanographic data collected by Argo profiling floats in the 
Ligurian Sea (French Riviera coast), 2018–2023.

## Motivation
A predictive model of this kind has practical applications in 
**quality control** of oceanographic data: when a float transmits a 
temperature reading, an automated pipeline can compare it against the 
model's prediction given the depth, salinity, location and time of year. 
A large discrepancy flags a likely sensor malfunction — more powerful 
than simple range checks because it accounts for physical context.

## Dataset
- **Source:** Argo Global Float Program (GDAC server)
- **Region:** Ligurian Sea, coast of Antibes, France (lon 6–8.5°E, lat 42.5–44.5°N)
- **Period:** 2018–2023
- **Size:** 125,099 depth profiles
- **Features:** depth, salinity, latitude, longitude, seasonality (cyclic encoding)
- **Label:** sea temperature (°C)

## Methodology
1. Data collection via the `argopy` Python library
2. Exploratory data analysis — histograms, boxplots, correlation heatmap, T-S diagram
3. Outlier analysis
4. Feature engineering — depth from pressure, cyclic month encoding
5. Train / validation / test split (60/20/20)
6. Z-score feature scaling
7. Linear regression baseline
8. Random Forest model
9. Overfitting check and final evaluation on held-out test set

## Results

| Model | RMSE (°C) | R² |
|---|---|---|
| Linear Regression | 0.767 | 0.408 |
| Random Forest | 0.089 | 0.993 |

The Random Forest predicts ocean temperature to within **0.09°C** on 
unseen data. Linear regression failed due to the highly non-linear 
thermal structure of the water column (thermocline).

## Key findings
- Depth accounts for ~70% of the model's predictive power, confirming 
the dominant role of the thermocline
- Seasonality is the second most important feature
- Geographic position had negligible predictive power within this small region

## Stack
Python · pandas · numpy · scikit-learn · matplotlib · seaborn · argopy

## Author
Berenger de Clers — 2nd year student, École des Mines de Paris
