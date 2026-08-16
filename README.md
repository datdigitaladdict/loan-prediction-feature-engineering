# Loan Prediction – Feature Engineering & Data Preprocessing

## AnalystLab Africa Data Science Internship – Week 2

This project focuses on **feature engineering and data preprocessing for machine learning** using the Loan Prediction dataset.

The objective is to transform the raw loan application data into a clean, numerical, and machine-learning-ready dataset that can be used to predict whether a loan application is likely to be approved.

---

## 1. Project Overview

### Business Problem

Financial institutions need to make loan approval decisions efficiently while reducing the risk associated with approving unsuitable applications.

A machine-learning model can learn patterns from historical loan applications and help predict the likely approval status of new applications.

### Project Objective

The objective of this project is to:

- Inspect the loan prediction dataset.
- Identify and handle missing values.
- Remove duplicate records.
- Validate and transform data types.
- Engineer useful features.
- Encode categorical variables.
- Detect and treat numerical outliers.
- Identify redundant and highly correlated features.
- Scale appropriate numerical features.
- Produce a final machine-learning-ready dataset.

### Target Variable

`Loan_Status`

- `1` = Loan approved
- `0` = Loan not approved

---

## 2. Dataset

The project uses the **Loan Prediction Dataset**.

The dataset contains information about loan applicants, including:

- Gender
- Married status
- Dependents
- Education
- Self-employment status
- Applicant income
- Coapplicant income
- Loan amount
- Loan term
- Credit history
- Property area
- Loan status

---

## 3. Technologies and Libraries

The project was completed using Python and Jupyter Notebook.

### Libraries

- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

### Main preprocessing tools

- `StandardScaler`
- IQR method
- Pandas data-cleaning functions
- Correlation analysis
- One-hot encoding

---

## 4. Project Workflow

The notebook follows this workflow:

```text
Data Loading
     ↓
Data Inspection
     ↓
Data Cleaning
     ↓
Feature Engineering
     ↓
Categorical Encoding
     ↓
Outlier Detection
     ↓
Outlier Treatment
     ↓
Correlation Analysis
     ↓
Feature Selection
     ↓
Feature Scaling
     ↓
Final Validation
     ↓
Machine-Learning-Ready Dataset
```

---

## 5. Data Preprocessing

### Missing Values

Missing values were assessed and handled during preprocessing.

The final validation confirmed:

```text
Total missing values: 0
```

### Duplicate Records

Duplicate records were checked during the workflow.

One duplicate record was identified during the final readiness check and removed.

Final result:

```text
Duplicate records: 0
```

### Data Types

Categorical variables were transformed into numerical representations.

The final validation confirmed:

```text
Non-numerical columns: 0
```

---

## 6. Feature Engineering

A new feature called `TotalIncome` was created by combining:

```text
ApplicantIncome + CoapplicantIncome
```

This provides a combined measure of the household income available for the loan application.

Correlation analysis later showed that `ApplicantIncome` and `TotalIncome` were strongly correlated (approximately **0.80**).

Because `TotalIncome` contains information already represented by applicant income, `ApplicantIncome` was removed during feature selection while `TotalIncome` was retained.

---

## 7. Categorical Encoding

Categorical variables were converted into numerical form so they could be used by machine-learning algorithms.

Binary categorical variables were represented using numerical values.

`Property_Area` was one-hot encoded into:

- `Property_Area_Semiurban`
- `Property_Area_Urban`

One-hot encoding was selected because property-area categories do not have a natural numerical ranking.

---

## 8. Outlier Detection and Treatment

Potential numerical outliers were detected using the **Interquartile Range (IQR)** method.

The conventional IQR boundaries were used:

```text
Lower Bound = Q1 - 1.5 × IQR
Upper Bound = Q3 + 1.5 × IQR
```

Potential outliers were identified in:

- ApplicantIncome
- CoapplicantIncome
- LoanAmount
- Loan_Amount_Term
- TotalIncome

### Outlier Treatment

IQR capping was applied only to the continuous financial variables:

- ApplicantIncome
- CoapplicantIncome
- LoanAmount
- TotalIncome

`Loan_Amount_Term` was not capped because it is a discrete loan-term feature with concentrated legitimate values. Treating it as a continuous variable could incorrectly modify valid loan terms.

---

## 9. Correlation Analysis

Correlation analysis was used to investigate relationships between the independent variables and the target variable.

### Strongest relationship with Loan_Status

`Credit_History` had the strongest individual correlation with loan approval:

```text
Correlation = 0.540556
```

This indicates a moderate positive relationship between credit history and loan approval status.

Other individual correlations were relatively weak.

However, weak Pearson correlation does not automatically mean that a feature is irrelevant. Machine-learning algorithms may identify nonlinear relationships and interactions that Pearson correlation does not capture.

---

## 10. Feature Selection

A correlation threshold of `|correlation| >= 0.70` was used to identify highly correlated independent features.

The analysis identified:

| Feature 1 | Feature 2 | Correlation |
|---|---|---:|
| ApplicantIncome | TotalIncome | 0.79562 |

Because `TotalIncome` was engineered from applicant and coapplicant income, keeping both `ApplicantIncome` and `TotalIncome` would introduce redundancy.

Therefore:

```text
ApplicantIncome → Removed
TotalIncome → Retained
```

The one-hot encoded property-area variables were retained because they represent different categories rather than duplicate measurements.

---

## 11. Feature Scaling

`StandardScaler` was applied to the following continuous numerical features:

- `CoapplicantIncome`
- `LoanAmount`
- `TotalIncome`

Standardization was selected because these financial variables have different numerical ranges.

After scaling:

```text
Mean ≈ 0
Standard deviation ≈ 1
```

The notebook confirmed that the scaled feature means were extremely close to zero and their standard deviations were approximately 1.

---

## 12. Final Dataset

After preprocessing and feature selection, the final dataset contains:

```text
Rows: 613
Columns: 13
```

### Final Features

1. Gender
2. Married
3. Dependents
4. Education
5. Self_Employed
6. CoapplicantIncome
7. LoanAmount
8. Loan_Amount_Term
9. Credit_History
10. Loan_Status
11. TotalIncome
12. Property_Area_Semiurban
13. Property_Area_Urban

`Loan_Status` is the target variable.

---

## 13. Final Machine-Learning Readiness Check

The final automated validation confirmed:

| Check | Result |
|---|---|
| Rows | 613 |
| Columns | 13 |
| Missing values | 0 |
| Duplicate records | 0 |
| Non-numerical columns | 0 |
| Target variable present | Yes |
| Machine-learning ready | Yes |

The dataset therefore passed the final preprocessing validation.

---

## 14. Visualizations

The notebook includes visualizations used to understand and validate the preprocessing process, including:

- Distribution visualizations
- Count plots
- Box plots
- Correlation heatmap
- Feature-target correlation visualization
- Post-treatment numerical feature visualization

These visualizations helped identify distributions, relationships, potential outliers, and feature importance patterns.

---

## 15. Repository Structure

The recommended GitHub repository structure is:

```text
Loan-Prediction-Feature-Engineering/
│
├── README.md
│
├── notebook/
│   └── Loan_Prediction_Feature_Engineering_Preprocessing.ipynb
│
├── data/
│   ├── Loan_Prediction_Cleaned_Dataset.csv
│   └── Loan_Prediction_Machine_Learning_Ready_Dataset.csv
│
├── reports/
│   ├── Business_Understanding_Report.docx
│   └── Data_Preprocessing_Report.docx
│
└── images/
    └── [project visualizations]
```

---

## 16. Key Findings

The main findings from the preprocessing analysis were:

1. `Credit_History` showed the strongest individual relationship with loan approval.
2. `ApplicantIncome` and `TotalIncome` were strongly correlated at approximately `0.80`.
3. `ApplicantIncome` was removed to reduce redundancy.
4. `TotalIncome` was retained as a combined income feature.
5. IQR capping was applied to continuous financial variables.
6. `Loan_Amount_Term` was excluded from IQR capping because it represents discrete loan-term categories.
7. `CoapplicantIncome`, `LoanAmount`, and `TotalIncome` were standardized using `StandardScaler`.
8. The final dataset contains 613 unique observations and 13 numerical columns.
9. The final dataset contains no missing values or duplicate records.
10. The dataset passed the machine-learning readiness check.

---

## 17. Skills Demonstrated

This project demonstrates practical experience with:

- Data cleaning
- Exploratory data analysis
- Feature engineering
- Feature selection
- Categorical encoding
- Outlier detection
- IQR-based outlier treatment
- Correlation analysis
- Feature scaling
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook
- Data documentation
- Machine-learning data preparation

---

## 18. Conclusion

The Week 2 project successfully transformed the Loan Prediction dataset into a machine-learning-ready format.

The preprocessing workflow addressed data quality issues, engineered a useful combined-income feature, encoded categorical variables, treated extreme financial values, removed redundant information, standardized selected numerical variables, and validated the final dataset.

The resulting dataset is ready for the next stage of the machine-learning workflow: **model development, training, evaluation, and comparison**.

---

## Author

**Onyinyechi Osuji**

Data Science Intern  
AnalystLab Africa Data Science Internship Programme

#AnalystLabAfrica
