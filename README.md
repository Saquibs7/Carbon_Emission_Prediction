# Carbon_Emission_Prediction
This Aicte affliated project aims analysis of country-specific data and development of machine learning models in order to predict CO2 emissions from country parameters.
## Stage 1: Data Cleaning and Preparation

This notebook is part of a larger machine learning project aimed at analyzing and predicting climate indicators, particularly **CO₂ emissions**, using **country-level data** provided by the [World Bank Climate Change Dataset](https://datacatalog.worldbank.org/dataset/climate-change-data).

---

## 📌 Stage 1 Objectives

The focus of Stage 1 is on **data cleaning**, **transformation**, and **feature enrichment** to prepare the dataset for exploratory analysis and predictive modeling.

### Key Goals:

- Clean and standardize raw climate data from multiple years and countries.
- Restructure the data to a **country-year-feature** format.
- Handle missing values and outliers systematically.
- Engineer new features relevant to climate modeling.
- Export both **cleaned** and **enriched** datasets for further use.

---

## 📁 Data Source

- **Source:** World Bank Climate Change Data
- **License:** [CC-BY 4.0](https://datacatalog.worldbank.org/public-licenses#cc-by)
- **Format:** `.xls` file, sheet `"Data"`

---

## 🧼 Data Cleaning Workflow

1. **Initial Inspection**
   - Identified missing values (`NaN`, `".."`, and blank entries).
   - Removed non-informative rows labeled `"Text"` in `SCALE` and `Decimals`.

2. **Column Reduction**
   - Dropped irrelevant columns: `Country name`, `Series code`, `SCALE`, and `Decimals`.

3. **Missing Values Handling**
   - Converted all missing value formats to `np.nan`.
   - Filtered out years and countries with high missing data (>90 entries).
   - Dropped features (columns) with >20 missing values.
   - Removed remaining rows with any missing values.

4. **Data Transformation**
   - Pivoted the long-format data into wide-format with each feature as a column.
   - Applied shorter, standardized names to features using a mapping dictionary.

---

## 🛠️ Feature Engineering & Improvements (Added)

To elevate the quality and modeling potential of the data, the following improvements were made:

### ✅ Outlier Detection & Removal
- Applied **IQR-based filtering** to remove extreme values from key numerical features (e.g., `co2_per_cap`, `gdp`, `en_per_cap`).

### ✅ New Engineered Features
- `co2_per_gdp_ratio`: Total CO₂ emissions per unit of GDP.
- `urbanization_rate`: Urban population as a ratio of total population.
- `gdp_per_capita`: GDP divided by total population.
- `co2_growth_rate`: Year-over-year CO₂ emission growth by country.

### ✅ Correlation Analysis
- Generated a heatmap to visualize the relationships between numerical features.

### ✅ Missing Data Visualization
- Used `missingno` to visualize missing patterns before and after cleaning.

---
# 🌍 Climate and Emissions Data Exploration – Stage 2

## 📑 Stage 2: Data Exploration and Visualization

This stage involves deep exploration and visualization of the cleaned climate and emissions dataset. It aims to derive insights, detect trends, outliers, and correlations that are relevant for hypothesis testing and future machine learning models.

---

### 📌 Goals:
- Understand data distributions, relationships, and trends.
- Define hypotheses around CO₂ emissions and potential predictors.
- Prepare variables and visual assets for model development.

---

### 🛠️ Notebook Contents

1. **Data Import & Setup**  
   Imported libraries and loaded the cleaned dataset (`data_cleaned.csv`).

2. **Global Overview**  
   - Dataset shape: `(1700, 18)`
   - Printed descriptive statistics, column types, and sample rows.
   - Checked for and removed missing values (newly added step).

3. **Feature Engineering**  
   - Created `en_ttl` (total energy use)
   - Applied `log` transformation to skewed features like `gdp`, `pop`, `co2_ttl`, etc. (improvement).
   - Removed less informative features based on correlation and VIF analysis.

4. **Hypothesis**  
   > _CO₂ emissions per capita can be predicted using features like energy use, GDP, urbanization, etc._

5. **Correlation and VIF**  
   - Computed and plotted correlation matrix
   - Selected best features by removing high VIF columns

6. **Visualizations**
   - Global average CO₂ per capita (1991–2008)
   - CO₂ vs population
   - Country-specific trends (USA, India, etc.)
   - Bubble plots with 4D data encoding
   - Pairplots for all relationships
   - Annotated scatterplots for top emitters (improvement)
   - Removed outlier country UAE to enhance trend clarity

---

### 🚀 Improvements Added

| Improvement | Description | Code Location |
|------------|-------------|----------------|
| ✅ Missing value handling | Explicitly checked and removed missing data | After data import |
| ✅ Log transformation | Applied to highly skewed numerical columns | Before correlation matrix |
| ✅ Annotated scatterplots | Added labels to major emitters in visualizations | In scatterplot section |

---

### 📈 Key Insights

- `co2_per_cap` is the best target variable: normalized, meaningful, and strongly correlated with energy use.
- High multicollinearity detected in some features; resolved with VIF filtering.
- Visuals reveal trends, outliers, and country-level behavior differences.
- Recommended model: Random Forest (nonlinear and robust to collinearity).

---

### 📁 Output Files
- `data_cleaned.csv`: Cleaned input data
- `stage2_exploration.ipynb`: Notebook with full code and visuals

---

> ✅ Proceeding to Stage 3: Model Development (Regression & Feature Importance)
## 📊 Features Used (After Selection)
- `cereal_yield`
- `gni_per_cap`
- `en_per_cap`
- `pop_urb_aggl_perc`
- `prot_area_perc`
- `pop_growth_perc`
- `urb_pop_growth_perc`

---

## 🚀 Key Enhancements

### ✅ 1. Feature Importances Visualization
- Understand which variables most influence predictions.
- Located after model training.

### ✅ 2. Train Set Evaluation
- Measures R², MSE, and RMSE on training data.
- Helps assess model overfitting.

### ✅ 3. Forecasted Results Export
- Saves 20-year predictions to `co2_forecast_20years.csv`..

### ✅ 4. Model Metadata Versioning
- Saves training metadata inside the `.pkl` file for future reference.

---
## 📦 Outputs
- `forecasting_co2_emmision.pkl`: Final trained model with metadata.
- `co2_forecast_20years.csv`: Forecasted CO₂ emissions for selected countries.
- `feature_importances.png`: Bar chart of variable importance.

---

## 📈 Model Performance
- **Cross-validated R²:** 0.986
- **Test R²:** 0.983
- **RMSE:** ~0.56 metric tons CO₂ per capita

---

## 📌 How to Run

1. Ensure you have Python 3.8+ and packages: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`.
2. Run `notebook.ipynb` from top to bottom.
3. Outputs will be saved in the same directory.

---

## ✨ Future Work
- Include more countries and years.
- Integrate real-time CO₂ tracking APIs.
- Train model ensembles or explore other regressors like XGBoost.

---
