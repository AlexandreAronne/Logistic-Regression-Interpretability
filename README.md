# Logistic Regression Interpretability Analysis

## Repository Overview

This repository contains a comprehensive analysis of logistic regression interpretability using American bankruptcy data. The project demonstrates various techniques for understanding and interpreting logistic regression models, including coefficient analysis, forward feature selection, and regularization approaches.

## Repository Structure

```
.
├── Interpretabilidade_Logistic_Regression_Insolvency_Github.ipynb
├── american_bankruptcy_dataset_new_light.xlsx
└── README.md
```

### Files Description

- **`Interpretabilidade_Logistic_Regression_Insolvency_Github.ipynb`**: Main Jupyter notebook containing the complete analysis workflow
- **`american_bankruptcy_dataset_new_light.xlsx`**: Dataset containing American bankruptcy information (13 MB)
- **`README.md`**: This documentation file

## Dataset

The analysis uses the American Bankruptcy Dataset, which contains:
- **Target variable**: `status_label` (alive → 0, failed → 1)
- **Features**: 18 numeric columns starting with `X` prefix
- **Size**: Approximately 13 MB of company financial data

The dataset tracks company insolvency status over multiple years and includes various financial metrics used to predict bankruptcy.

## Analysis Methodology

The notebook implements a comprehensive pipeline for logistic regression interpretability, organized in the following steps:

### 1. Data Preparation
- Loads bankruptcy data from Excel file
- Maps target labels (alive/failed) to binary values (0/1)
- Selects first 18 numeric features starting with 'X'
- Performs stratified train-test split (80-20 ratio)

### 2. Non-Standardized Logistic Regression
**Objective**: Establish baseline model performance with raw feature scales

- Trains unregularized logistic regression (penalty=None)
- Uses balanced class weights to handle class imbalance
- Generates coefficient plots to visualize feature importance
- Evaluates using multiple metrics: accuracy, precision, recall, F1, ROC-AUC, log loss

**Key Insight**: Coefficients on raw scales are difficult to compare due to different feature magnitudes.

### 3. Standardized Logistic Regression
**Objective**: Enable fair comparison of feature importance

- Applies StandardScaler to normalize all features (mean=0, std=1)
- Retrains logistic regression on standardized features
- Generates comparable coefficient plots
- Provides clearer interpretation of relative feature importance

**Key Insight**: Standardization allows direct comparison of coefficient magnitudes to assess relative feature impact.

### 4. Forward Feature Selection
**Objective**: Identify minimal subset of most predictive features

Two approaches implemented:
- **AIC-based selection**: Minimizes Akaike Information Criterion
- **BIC-based selection**: Minimizes Bayesian Information Criterion

Process:
1. Starts with no features
2. Iteratively adds features that most improve the criterion
3. Stops when no improvement is achieved
4. Tracks AIC, BIC, and performance metrics at each step
5. Generates plots showing model evolution

**Key Insight**: Forward selection helps identify which features are truly necessary for prediction.

### 5. Undersampling with Forward Selection
**Objective**: Handle class imbalance through data-level approach

- Identifies majority class (alive companies)
- Randomly undersamples majority to match minority class size
- Applies forward selection (both AIC and BIC) on balanced dataset
- Compares results with full dataset approach

**Key Insight**: Balanced datasets can lead to better minority class (bankruptcy) detection.

### 6. L1-Regularized (LASSO) Logistic Regression
**Objective**: Automatic feature selection through sparsity-inducing regularization

Tests four regularization strengths:
- C = 0.001 (strongest regularization, most sparse)
- C = 0.01 (strong regularization)
- C = 0.1 (moderate regularization)
- C = 1.0 (light regularization)

For each C value:
- Trains L1-penalized model
- Counts non-zero coefficients
- Generates coefficient plots
- Evaluates performance metrics

**Key Insight**: LASSO automatically shrinks less important feature coefficients to zero, providing built-in feature selection.

### 7. Temporal Analysis
**Objective**: Understand how bankruptcy patterns change over time

- Auto-detects year column (fyear, year, Year, FYEAR, or datetime)
- Generates stacked bar plot showing solvent vs. insolvent firms by year
- Visualizes potential trends in bankruptcy rates

## Key Features

### Visualization Capabilities
1. **Horizontal Coefficient Bar Plots**
   - Sorted by absolute magnitude
   - Symmetric x-axis centered on zero
   - Optional odds-ratio secondary axis (exp(coefficient))
   - Hover tooltips when mplcursors is available
   - Clear positive/negative coefficient distinction

2. **Metric Evolution Plots**
   - Track AIC/BIC during forward selection
   - Monitor accuracy, precision, recall, F1, ROC-AUC
   - Visualize tradeoffs between model complexity and performance

3. **Temporal Distribution Plot**
   - Stacked bar chart of class distribution by year
   - Helps identify temporal trends in bankruptcy patterns

### Model Evaluation Metrics
The analysis comprehensively evaluates models using:
- **Accuracy**: Overall correctness
- **Precision**: Positive prediction accuracy
- **Recall**: True positive detection rate
- **F1 Score**: Harmonic mean of precision and recall
- **ROC-AUC**: Discrimination ability
- **Log Loss**: Probabilistic prediction quality
- **AIC/BIC**: Model complexity vs. fit tradeoff

## Technical Configuration

### Dependencies
```python
- pandas
- numpy
- matplotlib
- scikit-learn (LogisticRegression, StandardScaler, metrics)
- openpyxl or xlrd (for Excel file reading)
- mplcursors (optional, for interactive tooltips)
```

### Key Parameters
- `RANDOM_STATE = 42`: For reproducibility
- `TEST_SIZE = 0.2`: 80-20 train-test split
- `X_TARGET_COUNT = 18`: Number of features to use
- `penalty = None`: Unregularized MLE (maximum likelihood estimation)
- `solver = 'lbfgs'`: Optimization algorithm
- `class_weight = 'balanced'`: Automatic class imbalance handling

## Usage Instructions

### Prerequisites
1. Install Python 3.x
2. Install required packages:
```bash
pip install pandas numpy matplotlib scikit-learn openpyxl
# Optional: pip install mplcursors
```

### Running the Analysis

1. **Clone the repository** (if not already done):
```bash
git clone https://github.com/AlexandreAronne/Logistic-Regression-Interpretability.git
cd Logistic-Regression-Interpretability
```

2. **Launch Jupyter Notebook**:
```bash
jupyter notebook
```

3. **Open the notebook**:
   - Navigate to `Interpretabilidade_Logistic_Regression_Insolvency_Github.ipynb`

4. **Update the file path** (cell 2):
```python
# Change this line to point to your data file
CSV_PATH = "american_bankruptcy_dataset_new_light.xlsx"
```

5. **Run all cells sequentially** to execute the complete analysis

### Customization Options

You can modify the analysis by adjusting:
- `X_TARGET_COUNT`: Number of features to include
- `TEST_SIZE`: Train-test split ratio
- `RANDOM_STATE`: Random seed for reproducibility
- Regularization strengths (`Cs` list in L1 section)
- Forward selection criterion (AIC vs BIC)

## Interpretability Insights

### What Makes This Analysis Interpretable?

1. **Coefficient Visualization**: Clear visual representation of feature impact direction and magnitude
2. **Standardization**: Enables fair comparison across features with different scales
3. **Feature Selection**: Identifies minimal feature sets that maintain predictive power
4. **Regularization Paths**: Shows which features remain important under different regularization strengths
5. **Multiple Perspectives**: Combines several approaches (forward selection, LASSO, undersampling) for robust insights

### Practical Applications

- **Credit Risk Assessment**: Identify key financial indicators of bankruptcy
- **Model Simplification**: Reduce model complexity while maintaining performance
- **Feature Engineering Guidance**: Understand which types of features matter most
- **Regulatory Compliance**: Provide interpretable models for financial decisions
- **Business Intelligence**: Communicate model insights to non-technical stakeholders

## Research Context

This analysis demonstrates best practices for interpretable machine learning in finance:
- **Transparency**: All model decisions can be explained through coefficients
- **Validation**: Multiple evaluation metrics ensure robust assessment
- **Reproducibility**: Fixed random seeds and clear methodology
- **Comparison**: Multiple approaches allow validation of findings

## Limitations and Considerations

1. **Linear Assumption**: Logistic regression assumes linear relationships in log-odds space
2. **Feature Interactions**: Basic model doesn't capture complex feature interactions
3. **Temporal Dependencies**: Standard train-test split may not account for time-based patterns
4. **Undersampling Tradeoff**: Loses majority class information
5. **Threshold Sensitivity**: Default 0.5 threshold may not be optimal for imbalanced data

## Future Extensions

Potential enhancements to this analysis:
- Cross-validation for more robust performance estimates
- Time-series aware splitting for temporal data
- Interaction term exploration
- Alternative resampling methods (SMOTE, ADASYN)
- Decision curve analysis for threshold optimization
- Partial dependence plots for feature interpretation
- Model calibration analysis

## Citation

If you use this repository in your research, please cite:
```
AlexandreAronne. (2024). Logistic Regression Interpretability Analysis.
GitHub repository: https://github.com/AlexandreAronne/Logistic-Regression-Interpretability
```

## License

Please check the repository for license information.

## Contact

For questions or issues, please open an issue on the GitHub repository.

---

**Note**: This analysis is for educational and research purposes. Financial decisions should not be made solely based on these models without proper validation and expert consultation.
