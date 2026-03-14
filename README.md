# Property-Price-Prediction-Engine
Enhanced Version:
https://colab.research.google.com/drive/1WtOd6OGs6ikV_FCXgNwmCa0E_qL4oJ0_?usp=sharing

Project Link:
https://colab.research.google.com/drive/1-LmP9vGLCDNmFMG2eYQ0lp1pzXSFfh-u#scrollTo=EpurokyHFY8X

# Property Price Prediction Engine

## Overview
This project implements an end-to-end machine learning pipeline to predict residential property prices using the **XGBoost Regressor**.  
The pipeline includes data preprocessing, feature engineering, hyperparameter optimization, experiment tracking, and feature storage.

The goal of the project is to simulate a **production-style ML workflow** rather than just a simple model training script.

Initial baseline models achieved an **R² score of ~0.56**, which was improved to **~0.80** after applying feature engineering, better encoding strategies, and model optimization.

---

## Dataset
The dataset (`realestatedata.xlsx`) contains residential property listings with features such as:

- `price`
- `house_size`
- `bed`
- `bath`
- `acre_lot`
- `city`
- `state`
- `zip_code`
- `status`
- `street`
- `brokered_by`

The dataset is included in this repository.

---

## Machine Learning Pipeline

### 1. Data Preparation
- Cleaned and standardized column names
- Removed rows with missing target values (`price`)
- Handled missing values using:
  - **KNN Imputation** for correlated numeric features
  - **Mode Imputation** for categorical features

---

### 2. Feature Engineering
Created domain-driven features to improve predictive power:

- `price_per_sqft` = price / house_size  
- `bed_bath_ratio` = bed / (bath + 1)  
- `lot_per_bed` = acre_lot / (bed + 1)

These features capture relationships between property characteristics that strongly influence price.

---

### 3. Target Encoding
High-cardinality categorical columns such as:

- `city`
- `state`
- `zip_code`
- `status`

were encoded using **target encoding**, replacing each category with the mean property price for that group.

This approach preserves location-based price patterns while avoiding large sparse matrices from one-hot encoding.

---

### 4. Model Training
The final model uses **XGBoost Regressor**, a gradient boosting algorithm well suited for tabular datasets.

Additional modeling steps include:

- **Log transformation of the target variable (`price`)** to reduce skew
- **StandardScaler applied only on the training data** to prevent data leakage

---

### 5. Hyperparameter Optimization
Model hyperparameters were tuned using **Optuna**, a Bayesian optimization framework that efficiently searches the parameter space.

Parameters optimized include:

- `n_estimators`
- `learning_rate`
- `max_depth`
- `subsample`
- `colsample_bytree`
- `min_child_weight`
- `gamma`
- `reg_alpha`
- `reg_lambda`

---

### 6. Feature Store
A lightweight **Parquet-based feature store** was implemented to persist processed features across experiments.

This enables faster experimentation without recomputing the entire preprocessing pipeline.

---

### 7. Experiment Tracking
Experiments are tracked using **MLflow**, which logs:

- Model hyperparameters
- Evaluation metrics
- Feature metadata
- Serialized model artifacts

This ensures full reproducibility and comparison across runs.

---

## Model Evaluation

Performance metrics used:

- **R² Score** – variance explained by the model  
- **MAE (Mean Absolute Error)** – average prediction error in dollars  
- **RMSE (Root Mean Squared Error)** – penalizes large prediction errors

