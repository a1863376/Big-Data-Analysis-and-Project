# Predicting Renewable Energy Generation in South Australia Using Weather Data

## Overview
This project is part of the Milestone 1D submission. The goal is to predict daily renewable energy generation (wind and solar) in South Australia based on weather features. Using machine learning models, particularly XGBoost and stacked ensembles, the study explores how weather variables influence renewable output and provides scenario-based strategies for energy planning.

The project also integrates clustering (KMeans) to identify typical weather patterns, linking them with generation outcomes to create actionable prescriptions for scheduling and system management.

## Research Question
**How can weather conditions be used to predict daily renewable energy generation in South Australia, and what operational strategies can be derived from these predictions?**

## Data
- **File provided:** `datasets.xlsx`
- **Content:**
  - Daily renewable energy generation (wind, rooftop solar, utility-scale solar)
  - Daily weather data (temperature, windspeed, solar radiation, humidity, UV index, cloud cover, precipitation)
- **Source:** Open Electricity Explorer (energy data), Visual Crossing (weather data)

## Methodology
The workflow follows several steps:
1. **Data Preprocessing:** Cleaning, imputation, and scaling  
2. **Feature Engineering:** Selecting weather-related predictors  
3. **Model Training:**
   - Baseline models (Linear Regression, Random Forest, XGBoost)
   - Separate models for wind and solar
   - Stacked ensemble model (best performing)
4. **Evaluation:** Train/test split, error metrics (R², RMSE, MAE)  
5. **Clustering:** K-Means clustering of weather features to generate scenario-based strategies  
6. **Visual Analysis:** Actual vs. Predicted plots, residual plots, SHAP value interpretation

## Main Results
- **Best Model:** Stacked XGBoost achieved the highest accuracy across prediction tasks
- **Feature Insights:** Solar radiation and wind speed are the most influential predictors
- **Scenario Strategies:**
  - Clear-sky days → battery charging opportunities
  - Windy/cloudy days → support from wind generation
  - Low wind/low solar days → demand response and maintenance scheduling

## How to Run
Install dependencies (main ones listed below):
```bash
pip install xgboost scikit-learn shap seaborn matplotlib pandas
```

Open and run the notebook:
- PartC_xgboost_final.ipynb (main version)
- Alternative versions: Part_C_xgboost.ipynb, PartC.ipynb (earlier drafts)
  
> [!TIP]
>  Visual results will automatically display during execution.

## Data Path Note
In the notebook we read the file like this:
```python
df = pd.read_excel("./datasets/datasets.xlsx", sheet_name="Sheet1")
```
This path assumes the file is inside a folder named datasets at the project root.
If your file is somewhere else, change the path accordingly:
- Same folder as the notebook
  ``` python
  df = pd.read_excel("datasets.xlsx", sheet_name="Sheet1")
  ```
- One level up
  ``` python
  df = pd.read_excel("../datasets.xlsx", sheet_name="Sheet1")
  ```
- Custom folder
  ``` python
  df = pd.read_excel("/full/path/to/datasets.xlsx", sheet_name="Sheet1")
  ```
> [!TIP]
> If you see FileNotFoundError, the path is wrong. Check the file location and adjust the string.\
> If you renamed the sheet, also update sheet_name="Sheet1".

## Outputs
- All key visualisations (Actual vs. Predicted plots, Residuals, SHAP plots, Clusters) are displayed when running the notebook
- Final results is included in the provided PDF: PartC_xgboost_final.pdf

## Limitations
- Weather data is limited to Adelaide, not all of South Australia
- Predictions are single-day, no multi-step forecasting
- Operational constraints (e.g., load, electricity price) not included
- Few samples of extreme weather conditions

## Future Work
- Extend the dataset with multiple locations and satellite data
- Develop multi-step forecasting models
- Integrate uncertainty quantification and scheduling optimization
