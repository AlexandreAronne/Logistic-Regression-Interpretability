# Quick Start Guide

Get up and running with the Logistic Regression Interpretability analysis in 5 minutes!

## Prerequisites

Ensure you have Python 3.7+ installed on your system.

## Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/AlexandreAronne/Logistic-Regression-Interpretability.git
cd Logistic-Regression-Interpretability
```

### Step 2: Install Dependencies
```bash
pip install pandas numpy matplotlib scikit-learn openpyxl
```

**Optional** (for interactive tooltips):
```bash
pip install mplcursors
```

## Running the Analysis

### Option 1: Jupyter Notebook (Recommended)

1. Start Jupyter:
```bash
jupyter notebook
```

2. Open `Interpretabilidade_Logistic_Regression_Insolvency_Github.ipynb`

3. Update the file path in Cell 2:
```python
CSV_PATH = "american_bankruptcy_dataset_new_light.xlsx"
```

4. Run → Run All Cells

### Option 2: JupyterLab

```bash
pip install jupyterlab
jupyter lab
```

Then open the notebook file.

### Option 3: VS Code

1. Install Python and Jupyter extensions in VS Code
2. Open the notebook file
3. Select Python kernel
4. Run all cells

## What You'll Get

The analysis will produce:

### 📊 Visualizations
- **Coefficient plots** showing feature importance
- **Metric evolution graphs** tracking model performance
- **Temporal distribution plots** of bankruptcy patterns
- **Comparison plots** across different modeling approaches

### 📈 Model Outputs
- **6 different modeling approaches**:
  1. Non-standardized logistic regression
  2. Standardized logistic regression
  3. Forward selection (AIC)
  4. Forward selection (BIC)
  5. Undersampled balanced models
  6. L1-regularized models (4 different strengths)

### 📋 Performance Metrics
For each model:
- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC
- Log Loss
- AIC/BIC (where applicable)

## Expected Runtime

| Hardware | Estimated Time |
|----------|---------------|
| Modern laptop/desktop | 1-3 minutes |
| Older hardware | 3-5 minutes |
| Colab/Cloud | 1-2 minutes |

## Troubleshooting

### Common Issues

**Issue**: `FileNotFoundError: american_bankruptcy_dataset_new_light.xlsx`
- **Solution**: Ensure the data file is in the same directory as the notebook
- Update `CSV_PATH` variable to the correct file location

**Issue**: `ModuleNotFoundError: No module named 'sklearn'`
- **Solution**: Install scikit-learn: `pip install scikit-learn`

**Issue**: `ModuleNotFoundError: No module named 'openpyxl'`
- **Solution**: Install openpyxl: `pip install openpyxl`

**Issue**: Plots not displaying
- **Solution**: Add `%matplotlib inline` to a cell before plotting cells

**Issue**: Memory error with large dataset
- **Solution**: This shouldn't occur with the 13MB dataset, but if it does, increase system RAM or use a subset of data

### Getting Help

1. Check the main [README.md](README.md) for detailed documentation
2. Review [ANALYSIS_SUMMARY.md](ANALYSIS_SUMMARY.md) for technical details
3. Open an issue on GitHub
4. Review the notebook comments for inline explanations

## Customization Quick Tips

### Change Number of Features
```python
X_TARGET_COUNT = 18  # Change to desired number
```

### Adjust Train-Test Split
```python
TEST_SIZE = 0.2  # Change to 0.3 for 70-30 split
```

### Modify Regularization Strengths
```python
Cs = [0.001, 0.01, 0.1, 1.0]  # Add more values: [0.0001, 0.001, 0.01, 0.1, 1.0, 10.0]
```

### Change Random Seed
```python
RANDOM_STATE = 42  # Change to any integer for different random splits
```

## Next Steps

After running the basic analysis:

1. **Explore Different Features**: Try selecting different feature subsets
2. **Experiment with Thresholds**: Test different classification thresholds (not just 0.5)
3. **Add Cross-Validation**: Implement k-fold CV for more robust estimates
4. **Try Your Own Data**: Adapt the notebook to your dataset
5. **Compare Models**: Add other model types (Decision Trees, Random Forests)

## Learning Path

### Beginner
- Run the notebook as-is to see outputs
- Read the markdown explanations between cells
- Focus on coefficient plots to understand feature importance

### Intermediate
- Modify parameters and observe changes
- Add additional evaluation metrics
- Experiment with different feature selection methods

### Advanced
- Adapt the code to your own dataset
- Implement additional interpretability techniques (SHAP, LIME)
- Create production pipelines from the analysis

## Resources

- **Main Documentation**: [README.md](README.md)
- **Technical Analysis**: [ANALYSIS_SUMMARY.md](ANALYSIS_SUMMARY.md)
- **Notebook**: `Interpretabilidade_Logistic_Regression_Insolvency_Github.ipynb`

## Quick Reference Card

```python
# Essential imports
import pandas as pd
import numpy as np
from sklearn.linear_model import LogisticRegression
from sklearn.preprocessing import StandardScaler

# Load data
df = pd.read_excel("american_bankruptcy_dataset_new_light.xlsx")

# Basic model
model = LogisticRegression(penalty=None, solver='lbfgs', random_state=42)
model.fit(X_train, y_train)

# Get predictions
predictions = model.predict(X_test)
probabilities = model.predict_proba(X_test)[:, 1]

# View coefficients
coefficients = model.coef_.ravel()
feature_importance = pd.Series(coefficients, index=feature_names).sort_values()
```

---

**Ready to Start?** Just run `jupyter notebook` and open the main notebook file! 🚀

For questions or issues, please refer to the main [README.md](README.md) or open an issue on GitHub.
