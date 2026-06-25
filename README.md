[README_Model_KNN.md](https://github.com/user-attachments/files/29339939/README_Model_KNN.md)
# Model KNN

Classification project using the `Social_Network_Ads` dataset. The goal is to predict whether a user will purchase a product after seeing an advertisement, based on socioeconomic information.

The repository compares a K-Nearest Neighbors classifier with a Logistic Regression baseline and also evaluates a modified Logistic Regression threshold using the ROC curve.

## Objective

Build and evaluate classification models that predict the `Purchased` variable from user information.

The project focuses on:

- Preparing the `Social_Network_Ads.csv` dataset.
- Encoding the categorical `Gender` feature.
- Exploring class balance and feature relationships.
- Training a KNN classifier.
- Training a Logistic Regression classifier.
- Comparing classification metrics.
- Optimizing the Logistic Regression decision threshold using ROC analysis.

## Repository Structure

```text
Model_KNN/
├── data_features.ipynb
├── models.ipynb
└── dataset/
    ├── Social_Network_Ads.csv
    └── Social_Network_Ads_procesados.csv
```

## Dataset

The repository includes:

- `dataset/Social_Network_Ads.csv`: original dataset.
- `dataset/Social_Network_Ads_procesados.csv`: processed dataset used for modeling.

The original dataset contains 400 records and the following fields:

- `User ID`
- `Gender`
- `Age`
- `EstimatedSalary`
- `Purchased`

The processed dataset replaces `Gender` with a dummy variable:

- `Gender_M`: `1` if the user is male, `0` otherwise.

The target variable is:

- `Purchased`: whether the user purchased the advertised product.

## Notebooks

### `data_features.ipynb`

This notebook performs the data preparation workflow:

- Loads the original dataset.
- Inspects missing values.
- Checks for duplicated records.
- Encodes `Gender` into `Gender_M`.
- Drops the original categorical `Gender` column.
- Reviews the class distribution of `Purchased`.
- Explores correlations between variables.
- Uses pair plots to inspect class separation.
- Saves the processed dataset as `Social_Network_Ads_procesados.csv`.

### `models.ipynb`

This notebook trains and evaluates:

- K-Nearest Neighbors classifier.
- Logistic Regression classifier.
- Logistic Regression with an optimized classification threshold.

## Technologies Used

- Python 3
- Jupyter Notebook
- pandas
- numpy
- seaborn
- matplotlib
- scikit-learn

## Installation

Clone the repository:

```bash
git clone https://github.com/fabriciolopretto/Model_KNN.git
cd Model_KNN
```

Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
.venv\Scripts\activate
```

Install the required dependencies:

```bash
pip install pandas numpy seaborn matplotlib scikit-learn jupyter
```

## Usage

Start Jupyter Notebook:

```bash
jupyter notebook
```

Run the notebooks in this order:

```text
data_features.ipynb
models.ipynb
```

`data_features.ipynb` creates the processed dataset, and `models.ipynb` trains and evaluates the classifiers.

## Methodology

1. Load `dataset/Social_Network_Ads.csv`.
2. Inspect the dataset for missing values and duplicates.
3. Encode `Gender` as `Gender_M`.
4. Save the processed dataset.
5. Load `dataset/Social_Network_Ads_procesados.csv`.
6. Select the predictors:
   - `Gender_M`
   - `Age`
   - `EstimatedSalary`
7. Use `Purchased` as the target variable.
8. Split the data into training and test sets with a 70/30 split, stratified by the target variable.
9. Standardize the input features with `StandardScaler`.
10. Train a KNN classifier with 25 neighbors.
11. Train a Logistic Regression model with balanced class weights.
12. Compare both models with confusion matrices and classification metrics.
13. Use the ROC curve and Youden's J statistic to choose an optimized Logistic Regression threshold.

## Models

### KNN Classifier

The KNN model uses:

```text
n_neighbors: 25
metric: minkowski
p: 2
```

### Logistic Regression

The Logistic Regression model uses:

```text
random_state: 0
class_weight: balanced
```

### Logistic Regression With Optimized Threshold

The notebook computes a ROC curve and selects the threshold that maximizes Youden's J statistic:

```text
best_threshold: 0.373802
```

## Results

The notebook reports the following metrics:

| Metric | KNN | Logistic Regression | Logistic Regression, Optimized Threshold |
| --- | ---: | ---: | ---: |
| Sensitivity | `0.7674` | `0.8140` | `0.8140` |
| Specificity | `0.9610` | `0.8442` | `0.8442` |
| Balanced Accuracy | `0.8642` | `0.8291` | `0.8291` |
| Precision | `0.9167` | `0.7447` | `0.6885` |
| Recall | `0.7674` | `0.8140` | `0.9767` |
| F1-score | `0.8354` | `0.7778` | `0.8077` |

KNN achieves the highest balanced accuracy and precision in this run. Logistic Regression identifies more positive purchase cases, especially after applying the optimized threshold, which increases recall and F1-score.

## Notes

The notebook observes that Logistic Regression performs better at identifying users who purchase the advertised product, while KNN performs better at identifying users who do not purchase it.

Because the target variable is somewhat imbalanced, balanced accuracy, recall, precision, and F1-score are more informative than plain accuracy alone.

