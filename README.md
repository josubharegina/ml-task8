# Phishing URL Detection using Machine Learning

## Project Overview

This project uses **Machine Learning** to classify URLs as either **legitimate** or **phishing**. The project is implemented in Python using a dataset containing URL-based features and a binary target label.

A **Linear Support Vector Machine (Linear SVM)** model is trained to detect phishing websites based on numerical characteristics extracted from URLs and webpage information.

## Dataset

The project uses:

`PhiUSIIL_Phishing_URL_Dataset.csv`

The dataset contains **26,764 records and 56 columns** in the notebook's preprocessing stage.

Some of the features include:

- URL length
- Domain length
- Whether the domain is an IP address
- TLD
- URL similarity index
- Character continuation rate
- TLD legitimate probability
- Number of subdomains
- Obfuscation features
- Number of letters and digits in URL
- HTTPS information
- Number of redirects
- Favicon information
- Robots information
- Number of images, CSS and JavaScript files
- Number of external references
- `label` — target variable

The target labels represent legitimate and phishing URLs.

## Technologies Used

- Python
- Pandas
- NumPy
- Seaborn
- Matplotlib
- Scikit-learn
- Google Colab / Jupyter Notebook

## Machine Learning Workflow

### 1. Import Libraries

The notebook imports NumPy, Pandas, Seaborn and Matplotlib for data processing and visualization.

Scikit-learn is used for:

- Train-test splitting
- Feature scaling
- Linear SVM
- Model evaluation
- Confusion matrix
- ROC curve

### 2. Load the Dataset

The CSV file is loaded using Pandas:

```python
df = pd.read_csv("/content/PhiUSIIL_Phishing_URL_Dataset.csv")
```

The dataset shape and column names are inspected.

### 3. Data Preprocessing

The notebook performs the following preprocessing steps:

- Checks for missing values.
- Removes rows where the target `label` is missing.
- Converts the target into a binary classification target.
- Removes non-numeric/text URL columns:
  - `URL`
  - `Domain`
  - `TLD`
  - `Title`
- Keeps numerical features.
- Replaces infinite values with missing values.
- Fills missing numerical values using the median.

After preprocessing, the feature dataset contains **50 numerical features**.

### 4. Train-Test Split

The data is divided into training and testing sets using an **80:20 split** with stratification.

- Training samples: **21,410**
- Testing samples: **5,353**

```python
train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42,
    stratify=y
)
```

### 5. Feature Scaling

`StandardScaler` is used to standardize the numerical features before training the model.

### 6. Model Training

The project uses a **Linear Support Vector Classifier (LinearSVC)**.

The model is created using a pipeline:

```python
make_pipeline(
    StandardScaler(),
    LinearSVC(
        C=1.0,
        class_weight="balanced",
        random_state=42,
        max_iter=5000
    )
)
```

The `class_weight="balanced"` option is used during training.

### 7. Prediction

The trained model predicts the labels of the test dataset.

The notebook also obtains the decision scores using:

```python
y_score = model.decision_function(X_test)
```

## Model Evaluation

The model is evaluated using:

- Confusion Matrix
- Precision
- Recall
- F1 Score
- ROC AUC
- Classification Report
- ROC Curve

### Confusion Matrix

The resulting confusion matrix is:

```text
[[3182    0]
 [   0 2171]]
```

The matrix uses:

- `0` = Legitimate
- `1` = Phishing

### Performance

The notebook reports:

| Metric | Score |
|---|---:|
| Precision | 1.0000 |
| Recall | 1.0000 |
| F1 Score | 1.0000 |
| ROC AUC | 1.0000 |
| Accuracy | 1.00 |

The classification report also shows a precision, recall and F1-score of **1.00** for both Legitimate and Phishing classes.

## Project Structure

```text
.
├── Task8_ML.ipynb
├── PhiUSIIL_Phishing_URL_Dataset.csv
└── README.md
```

## How to Run

1. Open `Task8_ML.ipynb` in Google Colab or Jupyter Notebook.
2. Upload `PhiUSIIL_Phishing_URL_Dataset.csv`.
3. Make sure the CSV path matches the path used in the notebook.
4. Run the notebook cells from top to bottom.
5. Review the preprocessing, model predictions and evaluation results.

## Conclusion

This project demonstrates a complete machine-learning workflow for **phishing URL detection**. The dataset is cleaned and transformed into numerical features, divided into training and testing sets, standardized, and used to train a **Linear SVM classifier**.

Based on the executed notebook results, the model achieved **1.00 accuracy, precision, recall, F1 score and ROC AUC** on the test set, with no misclassifications shown in the confusion matrix.
