# Study of Factors Affecting Marital Status and Comparison of k-NN, classification Tree and Naïve Bayes Methods

This repository presents an analysis that applies machine learning techniques to classify **marital status (married or not)** using the **Determinants of Wages Data (CPS 1985)**. The study compares three classification methods: **k-Nearest Neighbors (k-NN)**, **Classification Tree**, and **Naïve Bayes**, to determine which model performs best.

---

## 📌 Objective

- To classify marital status (married or not) using:
  - k-Nearest Neighbors (k-NN)
  - Classification Tree
  - Naïve Bayes
- To compare model performance and determine the most accurate method using **cross-validation** strategies.

---

## 📂 Dataset Information

- **Name:** Determinants of Wages Data (CPS 1985)  
- **Source:** [Kaggle – Avik Das](https://www.kaggle.com/datasets/avikdas2021/determinants-of-wages-data-cps-1985)  
- **Observations:** 534  
- **Variables:** 12 (5 quantitative, 7 categorical)  
- **Population:** Cross-sectional data from the May 1985 Current Population Survey (US Census Bureau)

### Variable Descriptions

| Variable      | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| wage          | Hourly wage in USD (continuous)                                             |
| education     | Years of education (continuous)                                             |
| experience    | Years of work experience (continuous)                                       |
| age           | Age of the individual (continuous)                                          |
| ethnicity     | Ethnic background: "hispanic", "cauc", "other"                              |
| region        | Location: "south", "other"                                                  |
| gender        | "male", "female"                                                            |
| occupation    | Job type: "worker", "technical", "services", "office", "sales", "management"|
| sector        | Employment sector: "manufacturing", "construction", "other"                 |
| union         | Union membership: "yes", "no"                                               |
| married       | Marital status: "yes" (married), "no" (not married)                         |

---

## Preliminary Data Analysis

- **Descriptive statistics** were computed using `summary()` in R.
- Variables were grouped into:
  - **Continuous:** `wage`, `education`, `experience`, `age`
  - **Categorical:** `ethnicity`, `region`, `gender`, `occupation`, `sector`, `union`, `married`
- **Visualizations** used:
  - Histograms, Boxplots for continuous variables
  - Bar charts and stacked charts for categorical variables

---

##  Methodology and Model Comparison

### ✅ k-Nearest Neighbors (k-NN)

- Variables used: `education`, `wage`, `experience`, `age`
- Tested different model versions:
  - Full model, Without `education`, Without `wage`, Without both
- Validation:
  - **Train/Test Split** (90/10 and 80/20)
    - Best accuracy: **0.7963** at K = 11 and 13 (90/10)
    - Best accuracy: **0.7477** at K = 15 and 17 (80/20)
  - **k-Fold Cross-Validation**
    - 10-fold: Best at K = 17, accuracy = **0.7099**
    - 5-fold: Best at K = 17 (without wage), accuracy = **0.7172**
- Conclusion: Removing some features slightly improved accuracy.

### ✅ Classification Tree

- Response: `married`
- Predictors: all variables
- Model trained and evaluated using **10-fold cross-validation** (before pruning)
- Pruning was avoided due to **underfitting**
- Best model: **nsplit = 5**, **xerror = 0.8370**, **accuracy = 0.7116**
  - Obtained by removing `wage`, `education`, and `age`

### ✅ Naïve Bayes

- Response: `married`
- Predictors:
  - Categorical: `ethnicity`, `region`, `gender`, `occupation`, `sector`, `union`
  - Discretized continuous: `wage`, `education`, `experience`, `age` using **Equal-Frequency Discretization**
- Evaluation: **10-fold cross-validation**
- Best model accuracy: **0.7064**  
  - Using discretized variables and sector

---

## Conclusion

| Method              | Best Accuracy (%) |
|---------------------|------------------|
| k-Nearest Neighbors | **79.63%**        |
| Classification Tree | 71.16%            |
| Naïve Bayes         | 70.64%            |

📌 **Recommendation:**  
Based on model performance, we recommend using **k-NN with 90/10 train-test split** as it achieves the highest classification accuracy.

---



