# Predicting Heart Disease Risk Using Machine Learning: An Exploratory and Comparative Analysis

An end-to-end data science and machine learning project that analyses clinical and behavioural patient records to investigate cardiovascular risk factors and predict heart failure risk. Developed as part of the MSc in Advanced Computer Science with Software Engineering at the University of Strathclyde.

## 📌 Project Overview
Cardiovascular diseases (CVDs) are the leading cause of mortality globally, accounting for an estimated 19.8 million deaths annually. Early diagnosis is vital for timely medical intervention. This project implements a comprehensive workflow, including data cleaning, exploratory data analysis (EDA), unsupervised clustering, and supervised binary classification to identify distinct patient risk profiles and predict the presence of heart disease.

## 📊 Dataset Structure
The project utilizes the **Heart Failure Prediction Dataset** (available on Kaggle), which integrates 5 independent heart datasets (Cleveland, Hungarian, Switzerland, Long Beach VA, and Stalog) across 11 shared features:

* **Total Records:** 1,190 observations (918 unique records after removing 272 duplicates).
* **Key Features Analysed:**
    * `Age` (Years)
    * `RestingBP` (Resting Blood Pressure in mmHg)
    * `Cholesterol` (Serum Cholesterol in mg/dL)
    * `FastingBS` (Fasting Blood Sugar: 1 if > 120 mg/dL, 0 otherwise)
    * `MaxHR` (Maximum Heart Rate Achieved)
    * `Oldpeak` (ST Depression Induced by Exercise Relative to Rest)
    * `Sex` (Categorical)
    * `ChestPainType` (Categorical)
    * `RestingECG` (Categorical)
    * `ExerciseAngina` (Categorical)
    * `ST_Slope` (Categorical)
    * `HeartDisease` (Target Class: 1 = Disease, 0 = Normal)

## ⚙️ Methodology & Pipeline

### 1. Data Preprocessing & EDA
* **Outlier Remediation:** Biological anomalies (such as `Cholesterol = 0 mg/dL`) and data entry errors in `RestingBP` were identified using boxplots and systematically removed, resolving scaling distortions during visualisations.
* **Correlation Analysis:** Feature correlation matrices revealed that no single attribute dominates prediction ($|r| < 0.5$ across all features), confirming that heart disease risk is inherently multifactorial. `Oldpeak` ($r = 0.40$) and `MaxHR` ($r = -0.40$) showed the strongest individual linear relationships.

### 2. Unsupervised Learning (Clustering)
* **Algorithm:** K-Means Clustering ($k=3$) applied purely to standardised numeric attributes.
* **Dimensionality Reduction:** 2D Principal Component Analysis (PCA) was used to project multi-dimensional feature boundaries.
* **Insights:** Evaluation yielded low completeness and homogeneity metrics ($ pprox 0.1 - 0.2$), graphically displaying overlapping clusters that reflect the complex, non-linear progression of clinical cardiovascular markers rather than discrete medical sub-populations.

### 3. Supervised Classifiers
* **Algorithm:** Logistic Regression, optimised for medical binary classification due to its direct probabilistic outputs (0 to 1).
* **Feature Encoding:** Categorical variables (`ChestPainType`, `RestingECG`, `ST_Slope`) were transformed via One-Hot Encoding, while binary fields (`Sex`, `ExerciseAngina`) were label-encoded.
* **Data Partitioning:** Split into 70% Training and 30% Testing subsets.

## 📈 Model Performance & Evaluation

The Logistic Regression model demonstrated exceptionally high diagnostic capabilities, striking an ideal balance between sensitivity and specificity:

* **Overall Accuracy:** 88%
* **Precision (Heart Disease = 1):** 0.92
* **Recall / Sensitivity (Heart Disease = 1):** 0.88
* **F1-Score:** 0.90
* **ROC-AUC Score:** 0.945 (94.5% probability of ranking a true positive patient higher than a healthy control)

### Confusion Matrix Breakdown
* **True Negatives (Correctly Identified Healthy):** 99
* **True Positives (Correctly Identified Sick):** 144
* **False Positives (Type I Error):** 13
* **False Negatives (Type II Error - Critical):** 20 (Kept minimal to prevent hazardous diagnostic omissions)

### Feature Significance & Odds Ratios
Using the exponential function on model coefficients, features were ranked by their contribution to the risk profile:
1.  **ST_Slope_Flat (Odds Ratio: 2.06):** Strongest positive clinical predictor of an active cardiac condition.
2.  **ExerciseAngina (Odds Ratio: 1.64):** Substantially increases heart failure probabilities.
3.  **Oldpeak (Odds Ratio: 1.63):** Significant ST depression indicators.
4.  **MaxHR (Odds Ratio: 0.96) & ChestPainType (Odds Ratio: 0.57):** Acted as statistically significant protective indicators (lower likelihood of failure).

## 🚀 Future Enhancements
* Implement advanced non-linear supervised ensembles, such as **Random Forests** and **Gradient Boosting (XGBoost)**, to capture intricate multi-variable clinical feature interactions.
* Incorporate supplementary, high-impact risk variables such as smoking habits, detailed dietary records, and genetic lineage data to improve generalisability across wider demographic populations.

## 📚 References
* American Heart Association (AHA). (2024). *What Your Cholesterol Levels Mean.*
* Fedesoriano. (2021). *Heart Failure Prediction Dataset.* Kaggle.
* Jolliffe, I.T. and Cadima, J. (2016). *Principal component analysis: a review and recent developments.* Philosophical Transactions of the Royal Society A.
* World Health Organization (WHO). (2023). *Cardiovascular diseases (CVDs) - Fact sheet.*
