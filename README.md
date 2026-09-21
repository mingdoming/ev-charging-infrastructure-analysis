# EV Charging Infrastructure Analysis

Priority Area Analysis for EV Charger Deployment based on XGBoost Prediction

## Overview

This project analyzes the regional supply-demand imbalance of EV charging infrastructure across 25 districts in Seoul.

Machine learning regression models were used to estimate the appropriate number of EV charging stations for each district. The difference between predicted and actual charger counts was then used to identify areas requiring additional infrastructure.

In addition, a policy priority score and K-means clustering were applied to support differentiated EV charging infrastructure planning.

## Research Objective

The main objectives of this study are:

- Predict the appropriate number of EV charging stations for each district
- Compare the performance of different regression models
- Identify regional supply-demand gaps using Out-of-Fold (OOF) predictions
- Calculate policy priorities for EV charging infrastructure expansion
- Classify districts into regional types using K-means clustering

## Study Area

The analysis was conducted for the **25 districts of Seoul, South Korea**.

The unit of analysis is each administrative district (gu).

## Dataset

Data from the Korean public data portal and Seoul Open Data Plaza were used.

### Target Variable

- Number of EV charging stations

### Predictor Variables

- Number of EVs
- Population
- Number of parking spaces
- Road length (m)
- Average monthly income
- Number of bus routes

The selected variables represent EV demand, population characteristics, physical infrastructure conditions, economic characteristics, and public transportation accessibility.

## Methodology

### 1. Data Preprocessing

The dataset was organized at the district level.

- Analysis units: 25 Seoul districts
- Missing values: None
- Train / Validation split: 80 / 20

### 2. Regression Models

Three regression models were compared:

- Ridge Regression
- Random Forest
- XGBoost

Model performance was evaluated using:

- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R² (Coefficient of Determination)

### 3. XGBoost Regression

XGBoost was selected as the main analytical model.

The model was used to capture nonlinear relationships between EV charging infrastructure and regional characteristics.

Feature importance analysis was also conducted to identify the variables contributing most to charger count prediction.

The analysis showed that the number of EVs and parking spaces were the most influential variables in predicting the number of charging stations.

## Model Performance

The three regression models were evaluated using the same set of variables.

| Model | MSE | RMSE | R² |
|---|---:|---:|---:|
| Ridge | 257,630.97 | 507.57 | 0.8067 |
| Random Forest | 358,235.62 | 598.53 | 0.7312 |
| XGBoost | 307,767.50 | 554.77 | 0.7691 |

Although Ridge Regression showed the highest R² value, XGBoost was selected as the final analytical model considering its ability to capture nonlinear relationships and interactions between regional characteristics and its applicability to policy-oriented analysis.

## OOF-Based Policy Priority Analysis

Out-of-Fold (OOF) prediction was used to estimate the appropriate number of EV charging stations for each district while reducing the risk of overly optimistic predictions from in-sample estimates.

The predicted charger count was compared with the actual number of installed chargers.

### Gap

The difference between predicted and actual charger counts was calculated as:

```text
Gap = Predicted Chargers - Actual Chargers

A positive gap indicates that the predicted infrastructure demand exceeds the current installation level.

### Policy Priority Score

A policy priority score was calculated using three standardized components:

- Shortage magnitude: 0.6
- Number of registered EVs: 0.3
- Population: 0.1

All components were standardized using z-scores to enable comparison across districts.

The top 30% of districts were further considered for recommended installation quantities based on shortage magnitude.

## Policy Priority Results

The OOF-based analysis identified several districts with relatively large gaps between predicted and actual charging infrastructure.

| District | Actual Chargers | Predicted | Gap | Shortage | Priority | Recommended |
|---|---:|---:|---:|---:|---:|---:|
| Gangbuk-gu | 915 | 1530.48 | 615.48 | 0.67 | 1.73 | 180 |
| Gwanak-gu | 1172 | 1781.95 | 609.95 | 0.52 | 1.43 | 160 |
| Guro-gu | 2545 | 3267.30 | 722.30 | 0.28 | 0.89 | 90 |
| Gangnam-gu | 4781 | 3752.17 | -1028.82 | 0.00 | 0.88 | 5 |
| Songpa-gu | 3948 | 4166.64 | 218.64 | 0.05 | 0.48 | 35 |

## K-means Clustering

K-means clustering was conducted to classify Seoul districts according to their regional characteristics.

The clustering variables included:

- Number of EVs
- Population
- Parking spaces
- Road length
- Average income
- Number of bus routes

The variables were standardized before clustering.

The optimal number of clusters was determined as **3** using the elbow method.

The resulting clusters were visualized spatially across Seoul to examine the distribution of regional types.

## Key Findings

The analysis identified regional differences in EV charging infrastructure supply and demand.

- EV registrations and parking spaces showed high importance in predicting charger counts.
- OOF predictions were used to estimate regional supply-demand gaps.
- Gangbuk-gu, Gwanak-gu, and Guro-gu showed relatively large predicted shortages.
- K-means clustering classified the 25 districts into three regional types.
- Combining prediction and clustering provides a framework for differentiated infrastructure planning.

## Research Publication

**Title:**  
XGBoost 기반 전기차 충전소 설치 예측에 따른 우선 설치 지역 분석

**English Title:**  
Priority Area Analysis for EV Charger Deployment based on XGBoost Prediction

**Authors:**  
So-min Yim, Ji-Hoon Seo

**Journal:**  
Journal of KIIT, Vol. 24, No. 2, 2026

**Keywords:**  
EV charging infrastructure, XGBoost, policy priority analysis, K-means clustering, EV charger deployment

## Technologies

- Python
- Pandas
- NumPy
- scikit-learn
- XGBoost
- Matplotlib
- GeoPandas

## Project Structure

```text
ev-charging-infrastructure-analysis/
├── README.md
├── 전기차분석(정보기술학회).ipynb
└── .gitignore
