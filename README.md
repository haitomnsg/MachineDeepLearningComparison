# Machine vs Deep Learning Comparison on Tabular Data

## Project Goal
This project compares one classical Machine Learning (ML) model and one Deep Learning (DL) model on tabular datasets.

Main question:
Can an explainable statistical ML model perform as well as, or better than, a DL model on tabular data?

## Scope and Rules
- Only tabular data (no image, audio, video, or text embeddings).
- Use one small dataset and one larger dataset.
- Use clean datasets that are ready to use.
- The exact same data split and preprocessing must be used for ML and DL.
- No data augmentation.
- No manual feature engineering.

## Final Dataset Selection

### 1) Small Dataset
- Name: Breast Cancer Wisconsin (Diagnostic)
- Source: UCI Machine Learning Repository (Dataset ID 17)
- Link: https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic
- Task: Binary classification
- Instances: 569
- Features: 30
- Missing values: No
- Why selected: Small, clean, numeric tabular dataset with a standard benchmark task.

### 2) Larger Dataset
- Name: Covertype
- Source: UCI Machine Learning Repository (Dataset ID 31)
- Link: https://archive.ics.uci.edu/dataset/31/covertype
- Task: Multiclass classification (7 classes)
- Instances: 581012
- Features: 54
- Missing values: No
- Why selected: Much larger in both rows and columns, still tabular and widely used for model comparison.

## Why This Pair Is Good for Comparison
- Same problem family: both are classification tasks.
- Clear scale gap:
  - Small: 569 x 30
  - Large: 581012 x 54
- Both are tabular and mostly numeric or integer features.
- Both are known benchmark datasets with clean metadata.

## Data Loading Plan
Use sklearn dataset loaders for consistent format:
- Small dataset: sklearn.datasets.load_breast_cancer
- Larger dataset: sklearn.datasets.fetch_covtype

This gives feature matrix X and target y in a standard structure for both ML and DL pipelines.

## Fair Comparison Protocol (Very Important)
To ensure the comparison is valid, both models must use exactly the same input data pipeline.

1. Set a fixed random seed.
2. Split each dataset into train, validation, test (for example 70/15/15) using stratification.
3. Fit preprocessing only on training data.
4. Apply the same transformed train/validation/test sets to all models.
5. No model-specific feature engineering.
6. No data augmentation.
7. Keep preprocessing minimal and identical (for example standard scaling).

Note: If Covertype training is too heavy on available hardware, use a fixed stratified subset once, then reuse that exact subset for every model.

## Baseline Models
To match the teacher requirement for explainable statistical ML:

- ML model (primary): Logistic Regression
  - Explainable coefficients and strong tabular baseline.

- DL model (primary): Multi Layer Perceptron (MLP)
  - Fully connected feed-forward neural network for tabular data.

Optional extra ML benchmark:
- Random Forest (for stronger non-linear ML baseline)

## Evaluation Metrics
Use the same metrics for both model families:
- Accuracy
- Macro F1 score
- Precision and Recall (macro)
- ROC-AUC
  - Binary AUC for Breast Cancer
  - One-vs-Rest macro AUC for Covertype
- Training time
- Inference time

## What to Report in Final Comparison
For each dataset, include:
- Best hyperparameters used
- Validation and test metrics
- Confusion matrix
- Training time comparison
- Short interpretation:
  - When did ML win?
  - When did DL win?
  - How does dataset size influence results?

## Recommended Project Structure
- README.md
- data
  - raw
  - processed
- notebooks
- src
  - data
  - models
  - train
  - evaluate
- reports

## Current Status
- Dataset selection: Completed
- Project README: Completed
- Next step: Implement a shared training and evaluation pipeline so both model types run on the exact same split and preprocessing.
