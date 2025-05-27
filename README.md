# 🛡️ Network Intrusion Detection System (NIDS) – Binary & Multiclass Modeling

## 🧾 Overview

This project implements a dual-phase **Network Intrusion Detection System (NIDS)** using the **NSL-KDD** dataset, a benchmark for evaluating cybersecurity algorithms. It includes:

- A **binary classification pipeline** to distinguish between *normal* and *attack* traffic.
- A **multiclass classification system** to further classify attacks into high-level threat categories: **DoS**, **Probe**, **Remote Access (R2L)**, and **Privilege Escalation (U2R)**.

The goal is to build a comprehensive machine learning-based detection system that not only identifies threats but also categorizes them, helping to simulate a real-world SOC (Security Operations Center) use case.

---

## 🚧 Problem Statement

With the exponential growth of digital connectivity, **network intrusion** has become a significant cybersecurity challenge. Most traditional systems either:

- Rely heavily on handcrafted rules (high false positive rate), or  
- Fail to adapt across different attack types or traffic conditions.

This project solves both problems by:
- Combining **feature engineering**, **statistical preprocessing**, and **ensemble ML models**.  
- Providing both **binary threat detection** and **attack-type classification**, aligned with practical SOC needs.

---

## 🧠 Project Highlights

### 🧪 Binary Classification
- Goal: Classify traffic as **attack vs. normal**
- Pipeline:
  - Categorical encoding (Protocol, Service, Flag)
  - Weight encoding for service frequency
  - PCA + Percentile-based feature selection
  - Ensemble modeling with:
    - Logistic Regression
    - Random Forest
    - Gradient Boosting
    - XGBoost
    - LightGBM
    - SVM
  - Grid Search CV for hyperparameter tuning
  - Voting ensemble for performance aggregation

### 🧬 Multiclass Classification
- Goal: Detect attack type:  
  `Normal | DoS | Probe | Remote Access (R2L) | Privilege Escalation (U2R)`
- Additional Steps:
  - **Class label restructuring** based on NSL-KDD attack families
  - **Outlier-aware transformation**: log-scaling of highly skewed features
  - Weighted categorical encodings + one-hot encoding
  - Correlation-driven feature selection using Spearman rank
  - Detailed **class-wise recall** and **confusion matrices**

---

## 📊 Model Evaluation

| Model            | Binary Accuracy | Multiclass Accuracy |
|------------------|-----------------|----------------------|
| Logistic Regression | ✅ High | ⚠️ Lower for U2R/R2L |
| Random Forest       | ✅ High | ✅ Good overall |
| Gradient Boosting   | ✅ High | ✅ Strong balance |
| XGBoost             | ✅ Best overall | ✅ Best for DoS |
| LightGBM            | ✅ Strong | ⚠️ Moderate R2L recall |
| SVM                 | ⚠️ Slower training | ⚠️ Poor U2R recall |
| ANN (multiclass only) | – | ✅ Excellent on "Normal" |

> 📈 **Multiclass recall analysis** showed U2R and R2L are the hardest to detect — consistent with real-world challenges.

---


---

## 📌 Key Techniques Used

- 🔄 **Label Restructuring**: Manual attack-to-category mapping for multiclass classification  
- 📊 **Log Transformation of Outliers**: For skewed count-based features  
- 🧼 **Weighted Encoding**: For services based on their frequency  
- 🧠 **PCA + Feature Selection**: Reduce dimensionality while preserving signal  
- ⚖️ **Ensemble Modeling**: Pipeline compatibility with both classifiers and meta-models  
- 📉 **Model Fit Diagnostics**: Custom overfit/underfit detection logic  
- 📈 **Cross-Validation**: Stratified K-Fold with performance logging  
- 🧪 **GridSearchCV Tuning**: Performed for every major model, including SVM, XGBoost, and LightGBM

---

## 🚀 How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/Adeleye-Emmanuel/Network-Intrusion-Detection
   cd Network-Intrusion-Detection
   
2. **Prepare your environment**
   ```bash
   pip install -r requirements.txt
   
3. **Run either notebook**

## Key Takeaways
🧠 Successfully built two distinct models for binary and multiclass NIDS

⚙️ Mastered data transformation, categorical encoding, and model pipelines

📊 Learned to evaluate not just accuracy, but recall per threat class

🧪 Tuned multiple classifiers with custom pipelines and cross-validation
