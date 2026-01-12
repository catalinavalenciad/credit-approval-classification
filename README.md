# Credit Approval Classification: Model Validation and Generalization Analysis

## Overview
This project demonstrates the design, validation, and comparison of **binary classification models** for an automated credit approval decision system. Using a real-world credit dataset, the analysis focuses on proper model validation, generalization performance, and methodological rigor, rather than relying solely on in-sample accuracy.

The project is structured as an end-to-end **credit risk modeling pipeline**, covering data preparation, imputation methodology, baseline model development, formal validation strategies, and final model selection using a held-out test set.

A central theme of this work is **model governance**: ensuring that tuning decisions are made without test-set leakage and that reported performance reflects true out-of-sample behavior.

## Business Problem
Credit approval is a high-stakes binary decision:

- Approve vs. reject an applicant  
- Low-risk vs. high-risk borrower  

Errors in these decisions have real financial consequences. While this project does not explicitly encode asymmetric costs, it focuses on robust validation design, which is a prerequisite for any cost-sensitive or regulated decision system.

The goal is to identify a classifier that generalizes well to unseen applicants under controlled and transparent evaluation conditions.

## Data Source
- **Credit Approval Dataset**  
  Public dataset from the **UCI Machine Learning Repository**  
  https://archive.ics.uci.edu/ml/datasets/Credit+Approval  

**Dataset characteristics:**
- This dataset is used without the categorical variables and without data points that have missing values
- 654 observations
- 10 numeric predictors
- 1 binary response variable (credit approval outcome)

The response labels are treated abstractly, and model performance is evaluated based on correct classification rather than semantic interpretation of approval vs. rejection.

## Tech Stack
- **Language:** R  
- **Environment:** RStudio  
- **Key Libraries:**  
  - `kernlab` (Support Vector Machines)  
  - `kknn` (k-Nearest Neighbors)  

## Methodology

### 1. Data Overview and Preparation
- Verified dataset structure, dimensionality, and class balance
- Confirmed absence of missing values in the original data
- Standardization of predictors to support:
  - Distance-based models (KNN)
  - Margin-based models (SVM)

No modeling decisions are made at this stage to avoid premature assumptions.

### 2. Missing Data & Imputation Study
Although the dataset is complete, missing data was artificially introduced to demonstrate and compare common imputation techniques:

1. **Mean imputation**
2. **Regression imputation**
3. **Regression with perturbation**

This analysis highlights how imputation choices can affect variance and downstream model behavior.  
After evaluation, the original complete dataset was retained for all final models to avoid unnecessary noise.

### 3. Baseline Classification Models
Two baseline classifiers were implemented:

1. **Model A: Support Vector Machine (Linear Kernel)**
   - Implemented using `ksvm`
   - Explored a wide range of regularization values (`C`)
   - Emphasized model stability and interpretability

2. **Model B: k-Nearest Neighbors (KNN)**
   - Implemented using `kknn`
   - Evaluated neighborhood sizes (`k = 1–20`)
   - Used leave-one-out cross-validation logic for baseline assessment

At this stage, performance reflects in-sample or LOOCV behavior only and is not used for final model selection.

### 4. Model Validation Strategies
To assess generalization and robustness, I applied:

1. **Method A: Cross-validation**
   - LOOCV for KNN
   - Stability analysis across hyperparameters

2. **Method B: Train / validation / test split**
   - 60% training
   - 20% validation
   - 20% test (held out until final evaluation)

Hyperparameters were selected exclusively using validation data, ensuring that the test set remained untouched until final model comparison.

### 5. Final Model Evaluation and Selection
After validation-based tuning:

- **Model A: SVM (Linear)**  
  - Best validation parameter: **C = 0.01**  
  - Test accuracy: **0.8626**

- **Model B: KNN**  
  - Best validation parameter: **k = 10**  
  - Test accuracy: **0.8779**

The final model comparison was conducted only on the held-out test set.

**Selected Model:** **KNN** (Model B)
While the performance difference is modest, KNN consistently achieved higher test accuracy under identical data splits and evaluation conditions.

## Results & Key Insights
- Validation design strongly influences perceived model performance.
- In-sample accuracy alone is insufficient for trustworthy deployment.
- Linear SVM offers interpretability but was slightly outperformed by KNN.
- KNN demonstrated strong generalization when properly tuned and validated.
- Transparent separation of training, validation, and test data is critical for model governance.

## Repository Structure

```
credit-approval-classification/
├── data/
│   └── credit_card_data.txt

├── notebooks/
│   ├── 01_data_overview_and_preparation.Rmd
│   ├── 02_imputation_study.Rmd
│   ├── 03_baseline_models.Rmd
│   └── 04_model_validation_and_selection.Rmd

├── docs/                     
│   ├── index.html         
│   ├── 01_data_overview_and_preparation.html
│   ├── 02_imputation_study.html
│   ├── 03_baseline_models.html
│   └── 04_model_validation_and_selection.html

├── README.md                
└── .gitignore
```

## Notes
This project prioritizes methodological correctness and reproducibility over optimization.  
All reported test results represent unbiased estimates of generalization performance.

---

## Contact
- **Name:** Catalina Valencia
- **Email:** catalinavalenciad@gmail.com
- **LinkedIn:** https://www.linkedin.com/in/catalina-valencia/
