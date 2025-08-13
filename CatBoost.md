# Tumor Classification with CatBoost

**Goal:** Read tumor feature data from a file and build an CatBoost classifier that predicts whether a tumor is *malignant* or *benign*.

---

## Table of contents

1. Problem statement
2. Required packages
3. Dataset and expected input file format
4. Step-by-step pipeline
   * Data loading
   * Train / validation split
   * Model training (XGBoost)
   * Evaluation
5. Example of Python script
6. Appendix: hyperparameter suggestions and metrics interpretation

---

## 1. Problem statement

You have a dataset (CSV, Excel, or similar) containing numeric features describing tumors (for example: Clump thickness,	Uniformity of Cell Size,	Uniformity of Cell Shape,	Marginal Adhesion,	Single Epithelial Cell Size,	Bare Nuclei, Bland Chromatin,	Normal Nucleoli,	Mitoses, etc.) and a target column indicating whether each tumor is `malignant` or `benign`. The task is to train an XGBoost classifier to predict the target label for new / unseen samples.

## 2. Required packages

```bash
pip install pandas numpy scikit-learn catboost
```
## 3. Dataset and expected input file format

The simplest expected format is a CSV file `tumors.csv` with rows = samples and columns = feature\_1, feature\_2, ..., feature\_n, target.

Example header:

```
Sample code number,Clump Thickness,Uniformity of Cell Size,Uniformity of Cell Shape,Marginal Adhesion,Single Epithelial Cell Size,Bare Nuclei,Bland Chromatin,Normal Nucleoli,Mitoses,Class
```

* `Class` should be text labels (`malignant` / `benign`) (e.g. `1` malignant, `0` benign). 

## 4. Step-by-step pipeline

### 4.1 Data loading

Load the file into a pandas DataFrame; examine columns and missing values.

### 4.2 Train / validation split

Use `train_test_split` (e.g., 80/20) and optionally use stratification to preserve class balance.

### 4.3 Model training (CatBoost)

* Use `catboost.CatBoostClassifier` for a straightforward API.

### 4.4 Evaluation

Report metrics:

* Accuracy
* Confusion matrix

## 5. Example of Python script
```
from catboost import CatBoostClassifier
classifier = CatBoostClassifier()
classifier.fit(X_train, y_train)
```

## 6. Appendix: hyperparameter suggestions and metrics interpretation

### Metrics explained briefly

* **Accuracy:** overall fraction correct. Can be misleading with imbalanced classes.
