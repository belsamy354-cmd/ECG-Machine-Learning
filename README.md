# ECG Classification using Machine Learning

## Project Overview

This project explores the use of Machine Learning to classify electrocardiogram (ECG) heartbeats as normal or abnormal.

The main objective is to compare classification algorithms, evaluate their performance, and analyze the factors influencing their predictions.

The project uses the PTB Diagnostic ECG Database dataset provided through the ECG Heartbeat Categorization Dataset on Kaggle.

## Dataset

The dataset contains **14,552 ECG heartbeats**, divided into two classes:

- **0:** Normal heartbeat
- **1:** Abnormal heartbeat

Each heartbeat is represented by **187 numerical features** corresponding to normalized ECG signal amplitudes.

The dataset is imbalanced, with more abnormal than normal heartbeats.


## Methodology

### 1. Exploratory Data Analysis (EDA)

We explored the ECG dataset to understand the distribution of normal and abnormal heartbeats.

Our analysis included:
- Visualization of ECG signals and average waveforms.
- Comparison of signal amplitudes and variability.
- Analysis of class imbalance.
- Identification of differences between normal and abnormal heartbeats.

### 2. Principal Component Analysis (PCA)

We applied PCA to explore the dimensionality of the ECG signals.

Key findings:
- The first two principal components explain approximately **51.63%** of the total variance.
- **37 components** preserve approximately 95% of the variance in the full dataset.
- PCA reduced the number of features used by KNN from 187 to 36 when fitted on the training set.

### 3. Machine Learning Models

We trained and evaluated two classification algorithms:

K-Nearest Neighbors (KNN)

Initial model with 5 neighbors.

KNN with PCA for dimensionality reduction.

Hyperparameter optimization using GridSearchCV.

Random Forest

Initial model with 100 decision trees.

Hyperparameter optimization using GridSearchCV.

Analysis of feature importance and classification errors.

4. Model Evaluation

We evaluated the models using:

Accuracy

Precision

Recall

F1-score

Confusion matrix

We paid particular attention to recall for abnormal ECGs, because false negatives are important in a medical classification context.

## Results

We compared several machine learning approaches on the ECG test dataset.

| Model | Accuracy | Precision | Recall | F1-score |
|---|---:|---:|---:|---:|
| KNN (k=5) | 92.99% | 96.07% | 94.15% | 95.10% |
| KNN + PCA | 93.34% | 95.82% | 94.91% | 95.36% |
| Optimized KNN (k=3) | 93.89% | 96.65% | 94.81% | 95.73% |
| Random Forest | 97.05% | 97.01% | 98.95% | 97.97% |
| Optimized Random Forest | **97.29%** | **97.16%** | **99.14%** | **98.14%** |

### Best Model: Optimized Random Forest

The best-performing model was a Random Forest classifier with:

- `n_estimators = 150`
- `max_depth = None`

On the test set of 2,911 ECG heartbeats, it achieved:

- 2,832 correct predictions
- 61 false positives
- 18 false negatives

### Feature Importance

The most important ECG signal positions identified by Random Forest were 4, 32, 3, 31, and 33.

These importance scores describe the model's use of the features and do not establish their clinical significance.

## Limitations

The dataset does not provide patient identifiers in the CSV files used in this project. Therefore, the random heartbeat-level train/test split does not guarantee patient-level independence.

The reported test performance may consequently overestimate generalization to unseen patients.

The project is intended for educational and experimental purposes, not clinical diagnosis.