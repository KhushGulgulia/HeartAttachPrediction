# Cardiovascular Health Data: ETL and Feature Engineering Pipeline

A data extraction, transformation, and exploratory analysis pipeline built on the composite UCI Heart Disease benchmark (918 patient observations). This project focuses on clinical data validation, physiological anomaly imputation, categorical encoding, and feature scaling.

---

## Dataset Overview

The pipeline processes clinical records from the combined UCI Heart Disease benchmark, aggregating patient records across five clinical studies (Cleveland, Hungarian, Switzerland, Long Beach VA, and Stalog).

- **Total Records:** 918 observations
- **Target Variable:** `HeartDisease` (1 = Present, 0 = Normal)
- **Feature Space:** 11 physiological, demographic, and electrocardiographic attributes

---

## ETL Pipeline Architecture

### 1. Extract
- Ingestion of raw comma-separated clinical vitals (`heart.csv`).
- Schema inspection, null-check validation, and duplicate detection.

### 2. Transform (Data Cleaning & Imputation)
- **Physiological Zero-Value Imputation:** 
  Clinical laboratory measurements contain zero values in serum cholesterol (`Cholesterol = 0`) and resting blood pressure (`RestingBP = 0`). Because these represent unrecorded measurements rather than true biological readings, they are imputed using the conditional median/mean of the non-zero cohort.
- **Categorical Feature Encoding:** 
  Nominal indicators (`Sex`, `ChestPainType`, `RestingECG`, `ExerciseAngina`, `ST_Slope`) are transformed using dummy variable encoding (`pd.get_dummies(drop_first=True)`) to eliminate multi-collinearity.
- **Continuous Feature Standardization:** 
  Continuous variables (`Age`, `RestingBP`, `Cholesterol`, `MaxHR`, `Oldpeak`) are normalized using z-score standardization (`StandardScaler`):
  
  $$z = \frac{x - \mu}{\sigma}$$

### 3. Exploratory Data Analysis (EDA)
- Univariate distribution analysis (KDE and histograms) for blood pressure, cholesterol, and age.
- Bivariate clinical correlation checks against heart disease outcomes across chest pain morphology, exercise-induced angina, and ST-segment depression (`Oldpeak`).

---

## Project Structure

```text
HeartAttachPrediction/
├── heart.csv            # Raw clinical benchmark dataset
├── heart.ipynb          # ETL, data cleaning, and feature engineering pipeline
├── .gitignore
└── README.md
```

---

## Dependencies & Setup

### Requirements
- Python 3.9+
- pandas, numpy, scikit-learn, matplotlib, seaborn

### Installation
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

### Running the Notebook
```bash
jupyter notebook heart.ipynb
```
