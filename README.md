# Credit Card Fraud Detection Pipeline

## Project Overview

This project is a machine learning model designed to accurately detect fraudulent credit card transactions. The main goal is to catch as much fraud as possible using a clean, step-by-step data processing pipeline.

## The Challenge

The biggest hurdle in this project is extreme class imbalance. Out of 284,807 transactions, about 99.83% are perfectly normal, while only 0.17% are actual fraud. Because of this, standard accuracy is not a good way to measure success, so the model is optimized to focus on PR-AUC (Precision-Recall Area Under the Curve) instead.

## How I Built It

To make sure the model learns fairly and doesn't cheat (data leakage), I processed the data in a strict order:

* **Data Splitting:** I split the data into training (80%) and testing (20%) sets before making any changes to the numbers.


* **Handling Outliers & Skewness:** The `Time` and `Amount` features had extreme values and were highly skewed. I built a custom tool to cap the extreme outliers and applied a mathematical transformation (Yeo-Johnson) to smooth them out.


* **Model Selection:** I used a Logistic Regression model to classify the transactions.


* **Handling Imbalance:** I applied a "balanced" class weight to the model, which forces it to pay much closer attention to the rare fraud cases.



## The Results

In banking, letting a fraudulent transaction slip through is much more expensive than occasionally flagging a normal transaction for review. The model's test results reflect this specific trade-off:

* **Recall (87.37%):** The model is great at finding the fraud. It successfully caught almost all fraudulent transactions, missing only 12 out of 95.


* **Precision (5.51%):** Because the model is highly sensitive to fraud, it generates a lot of false alarms, which is an expected and acceptable trade-off.


* **ROC-AUC:** 0.9620.


* **PR-AUC:** 0.6705.



## Next Steps to Improve the Model

To reduce the number of false alarms without missing actual fraud, future updates will include:

* **Threshold Tuning:** Adjusting the default 0.5 probability cutoff to find a better balance between false positives and false negatives.


* **Testing New Models:** Upgrading from Logistic Regression to tree-based models like Random Forest, XGBoost, or LightGBM.


* **Synthetic Data:** Using techniques like SMOTE or ADASYN to create fake fraud examples and balance the training data.


* **Feature Engineering:** Breaking down the `Time` column into more useful data points, like the specific hour of the day the transaction occurred.
