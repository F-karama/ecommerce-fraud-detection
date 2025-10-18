# 🛍️ E-commerce Fraud Detection

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.x-orange?logo=scikitlearn)
![XGBoost](https://img.shields.io/badge/XGBoost-Optimized-success?logo=xgboost)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 1️⃣ Background, Problem & Objectives

### 🧭 Background

With the rapid growth of online commerce, fraud has become a critical challenge for digital businesses.  
Companies must deploy **automated machine learning tools** to detect suspicious behavior early and secure transactions without harming the customer experience.

### ❓ Problem Statement

> How can we design a **machine learning model** capable of accurately detecting fraudulent e-commerce transactions while minimizing both false positives and false negatives?

### 🎯 Objective

To develop a **predictive classification model** that distinguishes legitimate transactions from fraudulent ones using **transactional, behavioral, and customer-related data**.

---

## 2️⃣ Data Overview

### 📦 Dataset Summary

* **18,000 transactions**
* **23 features** (numerical, categorical, textual)
* **Target variable:** `fraudulent` → 1 if fraud, 0 otherwise
* **Average fraud rate:** ≈ 7% (highly imbalanced dataset)

### 🧾 Key Variables

| Variable              | Type        | Description                                                         |
| --------------------- | ----------- | ------------------------------------------------------------------- |
| `transaction_amount`  | Numeric     | Transaction amount (€), median ≈ 54.9                               |
| `payment_method`      | Categorical | Payment method (card, paypal, bank_transfer, apple_pay, google_pay) |
| `ip_risk_score`       | Numeric     | IP risk score (0–100), 75% < 27.2                                   |
| `account_tenure_days` | Numeric     | Account age in days (~6.8 years on average)                         |
| `chargeback_history`  | Binary      | Previous chargebacks (strong indicator of fraud)                    |
| `num_items`           | Numeric     | Number of purchased items                                           |
| `customer_region`     | Categorical | Customer region (EU, NA, APAC, LATAM, ME)                           |
| `time_on_site_sec`    | Numeric     | Time spent on the website (seconds)                                 |

---

## 3️⃣ Methodology and Data Preparation

### 🧮 Workflow Summary

1. **Exploratory Data Analysis (EDA)**
   * Fraud rate highest for **Google Pay × Middle East (ME)** ≈ 14–15%.
   * Significant categorical variables: `chargeback_history`, `payment_method`, `interaction_bt_eu`.
   * No strong linear correlations among numeric variables (|r| < 0.7).

2. **Data Preprocessing**
   * **Missing values:** Added category `Unknown` for missing `customer_region` (25% missing).
   * **Feature cleaning:** Removed 6 uninformative variables (`transaction_id`, `astrological_sign`, etc.).
   * **Encoding & scaling:** One-Hot / Ordinal encoding for categorical features, normalization for numeric ones.

3. **Feature Selection**
   * Compared **Step Forward**, **Step Backward**, and **Genetic Algorithm**.
   * Genetic Algorithm achieved the best AUC (≈ 0.5814) with **35 selected features**.
   * Key features: `transaction_amount`, `ip_risk_score`, `num_previous_transactions`, `delivery_time_days`, `chargeback_history`.

---

## 4️⃣ Modeling & Interpretability

### ⚙️ Models Tested

* **K-Nearest Neighbors (KNN)**
* **Bagging (Decision Tree base)**
* **Random Forest**
* **XGBoost (optimized with GridSearchCV)**

### 🧠 Final Model: Optimized XGBoost

Chosen for its superior ability to capture weak fraud patterns and complex interactions.

#### 🔍 Model Interpretability (SHAP & Permutation Importance)

Most influential predictors:

* `account_tenure_days`
* `transaction_amount`
* `num_previous_transactions`
* `payment_method_bank_transfer`
* `customer_region_LATAM`
* `preferred_language_de`

---

## 5️⃣ Results & Strategic Insights

| Metric        | Value | Interpretation                        |
| ------------- | ----- | ------------------------------------- |
| **AUC ROC**   | 0.58  | Moderate discriminative power         |
| **Recall**    | 37%   | Model detects ~1 out of 3 frauds      |
| **Precision** | 9%    | 9% of fraud alerts are true positives |

### 💬 Conclusions

The final model performs moderately well given the data imbalance, but **should not be used as an automatic blocking system**.  
Instead, it serves as a **decision-support tool** to help fraud analysts prioritize high-risk cases.

### 🚨 High-Risk Transaction Profile

* Recent account (low `account_tenure_days`)
* High IP risk score
* Short session duration
* Payment via **bank transfer**
* Transaction amount between €100–300

### 🚀 Future Improvements

1. Add more behavioral and device-based features.  
2. Leverage customer transaction history for temporal analysis.  
3. Explore hybrid (supervised + unsupervised) fraud detection approaches.

---

## 6️⃣ Tools & Technologies

| Library / Tool           | Purpose                          |
| ------------------------ | -------------------------------- |
| **Python 3.10+**         | Main programming language        |
| **Pandas / NumPy**       | Data wrangling and preprocessing |
| **Scikit-learn**         | Modeling and evaluation          |
| **XGBoost**              | Final optimized model            |
| **SHAP**                 | Model explainability             |
| **Matplotlib / Seaborn** | Visualization                    |
| **Jupyter Notebook**     | Interactive workflow             |

---

