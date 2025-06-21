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

