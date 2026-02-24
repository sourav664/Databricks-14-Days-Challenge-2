# 🚀 Production-Grade Feature Engineering

## 📌 Overview

Production-grade feature engineering focuses on building reliable, scalable, and model-ready features that work consistently in both training and real-time inference.

This section covers:

- Target Creation
- Feature Selection
- Handling Imbalanced Data

---

# 1️⃣ Target Creation

## 📌 What is Target Creation?

The **target variable** (also called label) is what the model tries to predict.

In production systems, target creation must be:

✔ Clearly defined  
✔ Time-aware  
✔ Leakage-free  
✔ Consistent across retraining  

---

## 🔥 Example: Binary Purchase Prediction

Business Question:

> Will the user make a purchase in the next 7 days?

Target creation logic:

```python
target = 1 if user_purchased_within_7_days else 0
```

---

## ⚠ Common Production Mistake: Data Leakage

Wrong approach:

Using future data to create features.

Example:

Using total purchases of 2024 to predict January 2024 purchases.

❌ Model sees the future  
❌ Unrealistic accuracy  

---

## ✅ Correct Production Approach

Target must be created using:

- Strict time boundaries
- Only historical data
- Proper training window

Example:

```
Feature window: Jan–June
Target window: July
```

Never mix them.

---

## 🎯 Key Rule

Features must come from the past.  
Target must represent the future.

---

# 2️⃣ Feature Selection

## 📌 What is Feature Selection?

Feature selection is the process of choosing the most important variables for model training.

Why?

✔ Reduce noise  
✔ Improve performance  
✔ Reduce overfitting  
✔ Improve inference speed  

---

## 🔥 Example

Suppose you have:

```
user_id
last_login_time
country
browser_version
random_id
```

Does `random_id` help prediction?

❌ No predictive value  
❌ Remove it  

---

## 🧠 Methods for Feature Selection

### 1️⃣ Correlation Analysis
Remove highly correlated features.

Example:
If `total_spend` and `avg_spend` are almost identical → keep one.

---

### 2️⃣ Feature Importance (Tree Models)

Use:

- Random Forest
- XGBoost
- LightGBM

Check feature importance scores.

---

### 3️⃣ Statistical Methods

- Chi-square test
- ANOVA
- Mutual Information

---

### 4️⃣ Domain Knowledge

Business understanding matters.

Example:

- User tenure likely matters
- Internal ID numbers do not

---

## 🎯 Production Rule

Keep features that:

✔ Improve model performance  
✔ Generalize well  
✔ Are available during inference  

---

# 3️⃣ Handling Imbalanced Data

## 📌 What is Imbalanced Data?

When one class dominates the dataset.

Example:

Fraud detection:

- 98% Non-fraud
- 2% Fraud

Model may predict all as non-fraud and still get 98% accuracy.

But this is useless.

---

## ❌ Why It’s Dangerous

- Model ignores minority class
- Poor recall
- Misleading accuracy

---

## ✅ Production Solutions

### 1️⃣ Resampling

Oversampling:

- SMOTE
- Random oversampling

Undersampling:

- Remove majority samples

---

### 2️⃣ Class Weights

Assign higher penalty to minority class.

Example in XGBoost:

```python
scale_pos_weight = negative_class / positive_class
```

---

### 3️⃣ Better Metrics

Instead of accuracy, use:

✔ Precision  
✔ Recall  
✔ F1-score  
✔ ROC-AUC  
✔ PR-AUC  

---

### 4️⃣ Threshold Tuning

Default threshold = 0.5

In imbalanced problems:

Adjust threshold to improve recall or precision.

---

## 🔥 Example

If fraud detection probability = 0.3

Instead of threshold 0.5:

Use threshold 0.2 to detect more fraud cases.

---

# 🧠 Production Checklist

Before deploying a model:

✔ Is target leakage removed?  
✔ Are selected features available in real-time?  
✔ Is class imbalance handled properly?  
✔ Are correct evaluation metrics used?  
✔ Is inference latency acceptable?  

---

# 🎯 Interview One-Liner

"Production-grade feature engineering involves creating time-aware targets, selecting predictive and inference-safe features, and handling class imbalance using appropriate sampling strategies and evaluation metrics."

---

# 🏁 Final Takeaway

Notebook-level feature engineering focuses on experimentation.

Production-grade feature engineering focuses on:

- Stability  
- Scalability  
- Reproducibility  
- Business impact  

---