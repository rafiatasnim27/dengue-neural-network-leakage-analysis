Dengue Outcome Classification: Neural Network and Leakage Analysis

This project uses a Dhaka-based dengue dataset to build and compare machine-learning
models, including a neural network. The main focus is not only prediction, but also
understanding why the models achieved perfect performance.



## Dataset

- Source: [A Comprehensive Dengue Dataset of Bangladesh](https://data.mendeley.com/datasets/zdtc3n6xv2/3)
- Records: 1,000
- Region: Dhaka, Bangladesh
- License: CC BY 4.0
- Target variable: `Outcome`

The dataset includes demographic information, clinical measurements, symptoms,
blood-related features, and dengue test results.

## Project Workflow

1. Loaded and inspected the dataset.
2. Checked missing values, duplicates, and target distribution.
3. Performed exploratory data analysis.
4. Selected clinically relevant features.
5. Excluded NS1, IgG, and IgM to avoid direct target leakage.
6. Used a stratified train-validation-test split.
7. Preprocessed numeric and categorical features.
8. Built logistic regression, random forest, and neural-network models.
9. Evaluated models using accuracy, precision, recall, F1-score, ROC-AUC,
   confusion matrix, ROC curve, and precision-recall curve.
10. Investigated why all models achieved perfect performance.

## Models Used

| Model | Purpose |
| Logistic Regression | Simple interpretable baseline |
| Random Forest | Nonlinear model and feature importance |
| Neural Network | Keras/TensorFlow classification model |
| Decision Tree | Leakage and rule-discovery analysis |

## Neural Network Architecture

```text
Input Layer
→ Dense(32, ReLU)
→ Dropout(0.2)
→ Dense(16, ReLU)
→ Dropout(0.2)
→ Dense(1, Sigmoid)
```

- Loss: Binary cross-entropy
- Optimizer: Adam
- Early stopping: Validation AUC
- Task: Binary classification

## Main Finding

All models achieved 100% test accuracy and ROC-AUC of 1.0.

Further analysis showed that the target variable is perfectly determined by
body temperature:

```text
If Body_Temperature > 37.85°C → Outcome = 1
If Body_Temperature <= 37.85°C → Outcome = 0
```

A decision tree confirmed this rule and achieved test ROC-AUC = 1.0.

Therefore, the models learned the dataset’s hidden rule, not a real-world
dengue-diagnosis relationship.

## Why This Matters

High accuracy does not always mean a useful model. In this project, perfect
performance was caused by target leakage in the dataset-generating process.

This project demonstrates the importance of:

- Data quality
- Exploratory data analysis
- Leakage detection
- Honest model evaluation
- Responsible interpretation of machine-learning results

## Limitations

- The dataset appears to be synthetic or rule-based.
- Body temperature perfectly determines the target variable.
- The model cannot diagnose dengue.
- The model cannot decide hospital admission.
- The project should not be used for real medical decisions.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- TensorFlow
- Keras
- Google Colab
- Jupyter Notebook

## How to Run

1. Download the dataset from Mendeley Data.
2. Rename it as `dataset.csv`.
3. Open the notebook in Google Colab.
4. Upload `dataset.csv` when prompted.
5. Run all cells from top to bottom.

## License

This project is released under the MIT License.  
The dataset is licensed under CC BY 4.0 by its original authors.
