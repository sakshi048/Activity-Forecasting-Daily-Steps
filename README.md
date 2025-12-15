# 📊Daily Activity Forecasting using Time Series & Explainable AI

This repository contains an end-to-end machine learning pipeline for forecasting daily step counts using wearable time-series data and associated clinical features.  
The project was developed as part of a Machine Learning Intern assignment focused on Time Series Forecasting, Explainable AI (XAI), and Data Engineering.

---

##  📌 Project Overview

The objective is to predict daily step counts for the next 365 days while ensuring model interpretability and a clean, reproducible data pipeline.  
The solution combines a univariate time-series baseline with a multivariate explainable model to quantify the impact of clinical factors on activity levels.

---

## Data Pipeline & Feature Engineering

- Converted all timestamps to Python `datetime` objects
- Aggregated raw step events into continuous daily step counts
- Ensured no missing dates in the time series
- Integrated clinical attributes as daily snapshot features:
  - Age
  - Smoking status
  - Therapy indicator
- Created time-series features:
  - Lag features (steps at t-1)
  - Temporal ordering preserved (no data leakage)

> Note: Clinical feature fusion is intentionally simplified due to limited event-level timestamps in the provided dataset.  
> This design decision is documented in the supporting document.

---
## 🛠️ Tech Stack

- **Language:** Python  
- **Environment:** Google Colab  
- **Libraries:**  
  - pandas, numpy  
  - matplotlib  
  - scikit-learn  
  - Prophet  
  - InterpretML (EBM)

---
## Models Used

### Model 1 — Baseline Time Series Model
- Prophet (univariate)
- Uses only historical daily step counts
- Captures trend and seasonality
- Evaluation metrics:
  - RMSE
  - MAE
- Temporal train–test split

### Model 2 — Multivariate Explainable Model
- Explainable Boosting Machine (EBM) from `interpretML`
- Inputs:
  - Lagged step counts
  - Clinical features
- Advantages:
  - Strong performance
  - Built-in global explainability
- Evaluation:
  - RMSE & MAE comparison with baseline model

---

## Explainability

- Global feature importance extracted from EBM
- Clear interpretation of how clinical variables influence predicted step counts
- Explainability results included in the supporting documentation

---

## Forecast Output

The notebook generates a 365-day forecast with the following schema:

| Column Name        |             Description                  |
|--------------------|------------------------------------------|
| Date               | Forecast date                            |
| Predicted_Steps    | Final predicted daily step count         |
| Trend_Component    | Long-term trend component                |
| Exogenous_Impact   | Impact of clinical and non-trend factors |

---

## Scalability & Cloud Design

- Conceptual design supports scaling to 100,000+ patients
- Uses cloud-native components:
  - Object storage (e.g., AWS S3)
  - Secure access via IAM roles
- Includes a simulated cloud upload function (disabled by default)
- Detailed design explained in the scalability document

---

## Repository Structure

