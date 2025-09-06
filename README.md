# Property-Price-Prediction-Engine
Project Link:
https://colab.research.google.com/drive/1-LmP9vGLCDNmFMG2eYQ0lp1pzXSFfh-u#scrollTo=EpurokyHFY8X

# Property Price Prediction Engine

- **Project Overview:** Predicts house prices using XGBoost Regressor based on features such as location, house size, number of bedrooms and bathrooms, and lot size.  
- **Initial Performance:** Achieved an R² Score of 0.56. Optimizations improved it to 0.8.  
- **Optimizations Applied:**  
  - Removed irrelevant columns  
  - Used Target Encoding for categorical features instead of Label Encoding  
  - Feature engineering: `price_per_sqft`, `bed_bath_ratio`, `lot_per_bed`  
  - Switched from RandomForest to XGBoost Regressor  
- **Dataset:** `realestatedata.xlsx`, available in this GitHub repository, containing columns: `price`, `house_size`, `bed`, `bath`, `acre_lot`, `city`, `state`, `zip_code`, `status`, etc.  
- **Preprocessing Steps:** Cleaned column names, handled missing values, dropped irrelevant columns (`street`, `brokered_by`), target encoded categorical features, and created new features.  
- **Requirements:** Python >= 3.8; Libraries: pandas, numpy, scikit-learn, xgboost, matplotlib, seaborn. Install with:  
  ```bash
  pip install pandas numpy scikit-learn xgboost matplotlib seaborn

Usage: Load dataset using df = pd.read_excel("realestatedata.xlsx"), train the model, evaluate it, and visualize feature importance.

Key Outputs:
R² Score showing model performance
Predicted price for a sample house
Feature importance plot
Features: Handles missing values, categorical encoding, feature engineering, log-transform of the target variable, and visualizes feature importance.
Evaluation Example: R² Score: 0.8, Predicted Price: $450,000.00
Future Improvements: Add more features, hyperparameter tuning (GridSearchCV or Optuna), deploy as a web API for real-time predictions.

Author: Karanam Sumanth, B.E. in Information Technology, 2025
