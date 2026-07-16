# Ames Housing Price Prediction

Machine Learning project predicting residential house sale prices using advanced regression techniques, based on the classic **Ames Housing Dataset** (Ames, Iowa, USA).
https://www.kaggle.com/code/alexisbcook/exercise-introduction/notebook
---

## Overview

Real estate pricing is often inconsistent — human-set prices can be biased and inaccurate, manual analysis is time-consuming and data-intensive, and prices shift constantly with market trends. This project builds and compares multiple regression models to predict house sale prices based on 79 explanatory features describing residential properties, aiming to provide a more objective, data-driven approach to property valuation.

**Who benefits:**
- **Homeowners** — set realistic asking prices (avoid overpricing or underpricing)
- **Real estate investors** — identify good buy/sell opportunities and estimate ROI more accurately
- **Real estate platforms & agencies** — provide reliable price estimates without manual appraisal
- **The industry as a whole** — greater price transparency, fewer mispricing issues

---

## Dataset

| Detail | Description |
|---|---|
| Source | Ames, Iowa, USA |
| Collection period | ~2006–2010 |
| Rows | 1,460 |
| Columns | 81 (79 explanatory features + Id + target) |
| Target variable | `SalePrice` |
| File | `train.csv` |

The dataset describes house characteristics such as lot size, room counts, construction materials, year built, garage type, neighborhood, and more.

---

## Project Workflow

1. **Data Exploration** — inspect structure, identify missing values (`df.info()`, missing value report)
2. **Data Visualization** — analyze distribution of `SalePrice` and numerical features
3. **Data Preprocessing** — feature selection, missing value imputation, encoding
4. **Modeling** — train multiple regression models
5. **Model Evaluation** — compare model performance (MAE, RMSE, R²)
6. **Key Insight** — identify which features drive price the most
7. **Key Impact** — translate insights into actionable recommendations
8. **Prediction** — analyze prediction accuracy and error patterns

---

## Data Preprocessing

- **Feature selection**: dropped irrelevant identifier column (`Id`)
- **Missing values (numerical)**: imputed with **median** (e.g. `LotFrontage`, `MasVnrArea`, `GarageYrBlt`)
- **Missing values (categorical)**: NaNs carry real meaning (e.g. `PoolQC` NaN = *No Pool*, `Alley` NaN = *No alley access*) — handled accordingly, then encoded via **One-Hot Encoding**
- Final check confirmed **zero remaining missing values** across all 245 processed columns

**Key missing-value findings:**
- `PoolQC`: 99.5% missing → most homes have no pool
- `Alley`: 93.8% missing → most homes have no rear alley access
- `FireplaceQu`: 47.3% missing → roughly half of homes have no fireplace

---

## Modeling

Data split: **80% train / 20% test**

| Model |
|---|
| Linear Regression |
| Decision Tree |
| Random Forest (`n_estimators=265`, `max_depth=16`) |
| XGBoost (`n_estimators=100`) |

---

## Model Evaluation

| Model | MAE | RMSE | R² Score |
|---|---|---|---|
| Linear Regression | 20,485.45 | 49,257.88 | 0.6837 |
| Decision Tree | 27,102.47 | 42,223.85 | 0.7676 |
| Random Forest | 17,420.24 | 28,504.24 | 0.8941 |
| **XGBoost**   | **17,507.63** | **28,180.96** | **0.8965** |

**Best model: XGBoost** — achieves the lowest RMSE and highest R², indicating the most accurate and reliable predictions among all models tested.

---

## Key Insight — Feature Importance

Based on the top 10 most important features from the best-performing model:

1. **`OverallQual`** (overall quality) — by far the most important factor, with ~35% importance, significantly outweighing all other features. Overall construction and material quality is the single biggest driver of house price.

2. **Secondary factors** (~5–10% importance each):
   - `FullBath` — number of bathrooms
   - `GarageCars` — garage capacity
   - `KitchenAbvGr` — number of kitchens above grade
   - `GrLivArea` — above-ground living area

3. **Minor factors** (<5% importance):
   - `GarageType_Detchd` — detached garage type
   - `KitchenQual_TA` — average kitchen quality
   - `CentralAir_Y` — central air conditioning
   - `Neighborhood_SWISU` — specific neighborhood
   - `Exterior2nd_CmentBd` — exterior material

---

## Key Impact — Recommendations

**For Sellers**
- Prioritize improving overall house quality first
- Renovating bathrooms and garage can meaningfully increase value
- Kitchen and living area improvements also matter

**For Buyers**
- Focus on overall quality as the primary price driver
- Check bathroom count/condition, garage, and kitchen carefully
- Living area (especially usable space) affects price to a fair degree

**For Real Estate Developers**
- Invest most heavily in overall construction quality
- Allocate budget according to feature importance ranking
- Lower-impact features (e.g. certain exterior materials) may not need heavy investment

---

## Prediction Analysis

Analysis of prediction errors vs. actual price reveals:

- **Error grows with price** — the model's prediction variance increases for higher-priced homes
- **Homes under $200,000** — predictions are tight and reliable (errors cluster near zero)
- **Homes above $400,000** — prediction errors are noticeably larger
- Maximum observed prediction error: **±$150,000**
- Several **outliers** exist in the higher price range, with some homes both over- and under-valued significantly around the $300,000 mark

**Recommendation:** Use this model with caution for houses priced above $400,000. Predictions are most trustworthy in the **$100,000–$200,000** range.

---

## Summary

- **Error trend**: The model tends to make larger prediction errors as house prices increase, especially above $400,000
- **Notable findings**: Multiple outliers detected; typical prediction deviation of ±$150,000
- **Recommendations**: Gather more high-price home data; always consider additional context factors for expensive homes
- **Future improvement**: Collect additional training data focused on higher-priced properties to improve model robustness in that range

---

## Tech Stack

- **Language**: Python
- **Libraries**: pandas, numpy, matplotlib, seaborn, scikit-learn, XGBoost

---
## Presentation

Full presentation slides available here: [Presentation.pdf](Presentation.pdf)
## Team

| Name | ID |
|---|---|
| กนกพร เศรษฐ์สิทธิโชค | 67056005 |
| ธนนท์ วชิรไชยการ | 67056027 |
| วราภรณ์ อมรเวช | 67056066 |
| ศศิชา ศรสิทธิ์ | 67056073 |

*Machine Learning & Predictive Analytics — House Prices: Advanced Regression Techniques*
