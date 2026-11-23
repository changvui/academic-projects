# Obesity level prediction

Coursework project for **BMDS2003 Data Science** (Group 14). The goal was to predict a
person's obesity level from lifestyle and body measurements, and to compare how different
classifiers behave on the same cleaned data.

## Pipeline

1. Load the raw survey dataset and look at summary statistics
2. Remove duplicate rows
3. Standardise column headers and fix inconsistent labels
4. Boxplot analysis and statistical quantification of outliers
5. Encode features by type: label encoding for binary, ordinal encoding for ordered
   variables (such as frequency of eating between meals), one-hot encoding for nominal
6. Encode the target variable and scale the features with StandardScaler
7. Train/test split
8. Train three models with manual hyperparameter tuning:
   - Logistic Regression (tuning `max_iter`)
   - Decision Tree (tuning `max_depth`)
   - Random Forest
9. Compare accuracy and review per-class classification reports

## Files

| File | What it is |
|------|------------|
| `Group14_BMDS2003_Obesity_Model_Training.ipynb` | Full preprocessing and model training pipeline |
| `Group14_BMDS2003_Obesity_Predictor_Prototype.ipynb` | Small prototype that loads the trained model and predicts from user input |

## Note

The dataset is not included (it was distributed through the course). The notebook expects
the CSV in the path set at the top of the first notebook.
