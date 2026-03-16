# Bike-Sharing Demand Analysis & Promotion Strategy

A data-driven analysis of bike-sharing rental trends in Washington D.C. 
(2011–2012) using EDA, statistical testing, and Random Forest regression 
to predict ridership and trigger context-aware promotions during low-demand periods.

---

## Overview

This project examines how weather, time, and special events impact 
bike-sharing ridership. A Random Forest Regressor is trained to predict 
casual, registered, and total ride counts, outperforming a baseline 
Linear Regression model by ~20% in R².

Feature importance is validated using SHAP values, and a promotion 
threshold is derived from the ride count distribution to trigger 
targeted discounts during off-peak periods.

---

## Dataset

Download the Bike Sharing Dataset from Kaggle/UCI and place in project root:

- `hour.csv` — hourly ride records (2011–2012)

> Dataset link: https://www.kaggle.com/datasets/lakshmi25npathi/bike-sharing-dataset

---

## Repository Structure
```
bike-sharing-demand-analysis/
├── bike_sharing_analysis.ipynb   # Main Colab notebook
├── requirements.txt              # Python dependencies
└── README.md
```

---

## How It Works

### Step 1 — Exploratory Data Analysis
- Analyzes ride counts by hour, weekday, month, temperature
- Compares casual vs. registered user behavior patterns
- Visualizes seasonal trends and weather impact

### Step 2 — Feature Engineering
- Time markers: hour, weekday, month, year, holiday, working day
- Weather: temperature, apparent temperature, humidity, windspeed
- Identifies multicollinearity between features

### Step 3 — Modeling
- Trains Random Forest Regressors for casual, registered, and total ridership
- Compares against baseline Linear Regression
- Tunes hyperparameters via grid search
- Validates feature importance with SHAP values

### Step 4 — Promotion Threshold
- Fits normal distribution to ride count histogram
- Sets threshold at µ = 189.5
- Triggers discount promotions when predicted count < 189
- Applies seasonal adjustments to avoid over-triggering

---

## Results

| Model | Train R² | Test R² |
|-------|----------|---------|
| Casual | 0.98 | 0.92 |
| Registered | 0.99 | 0.95 |
| Total | 0.98 | 0.94 |

### Key Findings
- Hour, working day, temperature, and humidity are top predictors
- Casual users peak 10AM–5PM; registered users peak at commute hours
- Casual users are more sensitive to seasonal and weather changes
- Random Forest improves R² by ~20% over Linear Regression

---

## Promotion Strategy

| Scenario | Promotion |
|----------|-----------|
| Fall/Winter | Ride 5 consecutive days → win $50 Amazon gift card |
| Off-peak casual | 5% off (9PM–6AM weekdays) |
| Off-peak registered | 10% off off-hours, 5% off 11AM–2PM |
| Holidays | 5% off rides over 30 minutes |
| Cold days | 15% off with code WARMUP |
| Referrals | First 3 trips free for new users |

---

## How to Run

### Google Colab (Recommended)
1. Open `bike_sharing_analysis.ipynb` in Google Colab
2. Upload `hour.csv` when prompted
3. Run all cells in order

### Local
```bash
pip install -r requirements.txt
jupyter notebook bike_sharing_analysis.ipynb
```

---

## Requirements
```
pandas
numpy
matplotlib
seaborn
scikit-learn
shap
scipy
jupyter
```

---

## Key Technical Decisions

| Decision | Reason |
|----------|--------|
| Random Forest | Handles nonlinear interactions between weather and time |
| Grid search tuning | Optimizes estimators and max depth |
| SHAP values | Improves model interpretability |
| Normal distribution threshold | Data-driven promotion trigger |
| Seasonal threshold adjustment | Avoids over-triggering in winter |

---

## Limitations
- Dataset limited to Washington D.C. (2011–2012)
- No real-time weather or event data integration
- Promotion effectiveness not A/B tested on real users

---

## Future Work
- Integrate live weather APIs for real-time predictions
- Geospatial station-level demand analysis
- Apply framework to other cities and transport modes
- Machine learning powered promo delivery system

---

## Contact

**Raaghul Nataraj Kannan**
MS in Data Science — Arizona State University
