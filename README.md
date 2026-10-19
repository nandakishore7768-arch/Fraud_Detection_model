# Fraud Detection Using Machine Learning

A machine learning project for detecting fraudulent transactions using Random Forest and XGBoost. The project focuses on handling class imbalance, comparing classification models, and optimizing the decision threshold to improve fraud detection performance.

## Problem Statement

Fraud detection is an imbalanced classification problem in which fraudulent transactions represent a minority of observations. Models must identify fraudulent activity while minimizing false positives on legitimate transactions.

The objective of this project is to build and evaluate machine learning models that distinguish fraudulent from legitimate transactions using an appropriate classification threshold.

## Dataset

**Source:** [Fraud Detection Dataset — Kaggle](https://www.kaggle.com/datasets/sshriya08/fraud-detection-dataset)

The dataset was explored using descriptive statistics, frequency counts, and unique-value analysis to understand the data distribution and class imbalance.

## Tech Stack

- **Language:** Python
- **Data Analysis:** Pandas, NumPy
- **Machine Learning:** Scikit-learn, XGBoost
- **Class-Imbalance Handling:** imbalanced-learn (`imblearn`), SMOTE
- **Model Persistence:** Pickle

## Methodology

### 1. Exploratory Data Analysis

- Examined target-class distribution using `value_counts()`.
- Investigated distinct values using `unique()` and `nunique()`.
- Inspected the dataset to inform preprocessing and modelling decisions.

### 2. Data Preprocessing

Applied feature scaling and categorical encoding where required to prepare the data for model training.

### 3. Class-Imbalance Handling

Used **SMOTE (Synthetic Minority Over-sampling Technique)** from `imblearn` on the training data to address the underrepresentation of fraudulent transactions.

SMOTE was restricted to the training data to avoid introducing synthetic samples into validation and test datasets.

### 4. Model Training and Comparison

Trained and evaluated two tree-based classifiers:

- **Random Forest:** Established a baseline for comparison.
- **XGBoost:** Evaluated as an alternative and selected for the final model based on its observed performance.

### 5. Threshold Optimization

Selected a classification threshold of **0.494** using the validation dataset. The selected threshold was then used to evaluate the model on held-out test data.

### 6. Model Evaluation

Evaluated the final XGBoost model using accuracy, precision, recall, F1-score, and a confusion matrix.

## Results

### Final XGBoost Test Performance

| Metric | Score |
|---|---:|
| Accuracy | 97.58% |
| Precision | 97.45% |
| Recall | 78.05% |
| F1-score | 86.68% |

### Test Confusion Matrix

| Actual / Predicted | Legitimate | Fraudulent |
|---|---:|---:|
| Legitimate | 13,480 | 31 |
| Fraudulent | 333 | 1,184 |

### Key Findings

- Correctly identified **1,184 fraudulent transactions** in the test dataset.
- Generated **31 false positives**.
- Missed **333 fraudulent transactions**, highlighting an opportunity to improve fraud recall.
- Achieved **78.05% recall** for the fraudulent class.

These results demonstrate the trade-off between identifying fraud and minimizing incorrect fraud alerts.

## Repository Structure

```text
fraud-detection/
├── dataset/
│   └── Dataset files
├── notebooks/
│   └── Analysis and model development notebooks
├── model.pkl
└── preprocessing.pkl
```

- **`dataset/`** — Contains the project dataset.
- **`notebooks/`** — Contains exploratory analysis, preprocessing, model training, and evaluation work.
- **`model.pkl`** — Serialized final XGBoost model.
- **`preprocessing.pkl`** — Serialized preprocessing object used to prepare input features for inference.

## Model Artifacts

The trained model and preprocessing object are saved as pickle files for reuse without retraining from scratch.

For inference, input data must undergo the same preprocessing and feature ordering used during training.

**Security note:** Only load pickle files from trusted sources, as deserializing untrusted pickle files can execute arbitrary code.

## Future Improvements

- Develop a backend prediction API using FastAPI.
- Build a frontend for submitting transaction features and displaying predictions.
- Integrate the frontend and backend into a complete application.
- Containerize the application using Docker.
- Explore deployment and monitoring for real-world inference.

## Disclaimer

This project is intended for educational and portfolio purposes. Reported metrics reflect performance on the available held-out test dataset and do not guarantee equivalent performance on real-world transactions.
