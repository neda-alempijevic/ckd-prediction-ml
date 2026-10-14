# Chronic Kidney Disease Prediction — Machine Learning

A machine learning project that predicts whether a patient has chronic kidney disease (CKD) from routine clinical measurements. It covers the full workflow: exploratory data analysis, data cleaning, preprocessing, training three classifiers and comparing them with a held-out test set and cross-validation.

Final project for the *Artificial Intelligence* course, Singidunum University.

> The notebook text is written in Serbian; code, charts and results are language-independent.

## Dataset

- **Source:** Chronic Kidney Disease dataset, UCI Machine Learning Repository (`kidney_disease.csv`)
- **Size:** 400 patients, 24 features + 1 target (`ckd` / `notckd`)
- **Features:** a mix of numeric lab values (blood pressure, blood glucose, serum creatinine, hemoglobin, packed cell volume, white and red blood cell counts…) and categorical findings (hypertension, diabetes, appetite, anemia…)

## Workflow

1. **Exploratory analysis** – structure, class balance, age distribution, missing values per feature
2. **Data cleaning**
   - stripped stray spaces and tab characters from all categorical columns (e.g. `dm` contained `yes`, ` yes` and `\tyes` as three separate values)
   - converted `pcv`, `wc` and `rc` from text to numbers — they were loaded as strings because some entries contain `?`
3. **Correlation analysis** of numeric features
4. **Missing values** – median for numeric, mode for categorical features
5. **Encoding** of categorical features with `LabelEncoder`
6. **Train/test split** – 80/20 (`random_state=42`)
7. **Models** – Logistic Regression, K-Nearest Neighbors, Random Forest
8. **Evaluation** – accuracy, confusion matrix, 5-fold cross-validation

## Results

| Model | Test accuracy |
|---|---|
| Logistic Regression | 97.5% |
| KNN (k = 5), without scaling | 68.75% |
| KNN (k = 5), with `StandardScaler` | 97.5% |
| **Random Forest** (100 trees) | **100%** |

**5-fold cross-validation (Random Forest):** 98.75% mean accuracy (folds: 98.75%, 100%, 96.25%, 98.75%, 100%).

### Key observations

- **Feature scaling matters for distance-based models.** Without scaling, white blood cell count (`wc`, values in the thousands) dominates the distance calculation and KNN drops to 68.75%. After standardization it reaches 97.5%.
- **Data cleaning changed what the model sees.** Before cleaning, numeric lab values were label-encoded as categories and duplicate categories differed only by whitespace.
- **The test set is small (80 patients)**, so one misclassification changes accuracy by 1.25 percentage points. Cross-validation gives a more reliable estimate than the single 100% test score.

## Tech stack

Python · pandas · NumPy · scikit-learn · matplotlib · seaborn · Jupyter

## How to run

```bash
git clone https://github.com/<username>/ckd-prediction-ml.git
cd ckd-prediction-ml
pip install -r requirements.txt
jupyter notebook Chronic_Kidney_Disease_Prediction.ipynb
```

Keep `kidney_disease.csv` in the same folder as the notebook.

## Project structure

```
├── Chronic_Kidney_Disease_Prediction.ipynb   # analysis, models and results
├── kidney_disease.csv                         # dataset
├── requirements.txt
└── README.md
```

## Disclaimer

This is an educational project exploring machine learning on a public dataset. It is not a diagnostic tool and should not be used for medical decisions.

## Author

**Neda Alempijević** · Computer Science, Singidunum University
