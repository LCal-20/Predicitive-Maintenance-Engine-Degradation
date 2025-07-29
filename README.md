# Predicitive-Maintenance-Engine-Degradation
# 🚁 NASA Turbofan Engine RUL Prediction System

A comprehensive machine learning system for predicting Remaining Useful Life (RUL) of turbofan engines using the NASA C-MAPSS dataset. This system features advanced feature engineering, automated hyperparameter tuning, and detailed performance analysis.

## 🎯 Key Features

- **Complete Data Pipeline**: Automated data loading from NASA C-MAPSS format
- **Advanced Feature Engineering**: 100+ engineered features including rolling statistics, degradation indicators, and physics-based ratios
- **Intelligent Feature Selection**: Multi-criteria feature selection using correlation, mutual information, and coefficient of variation
- **Optimized XGBoost Model**: Automated hyperparameter tuning with 5-fold parameter search
- **Comprehensive Evaluation**: Multiple metrics including RMSE, MAE, R², and NASA scoring function
- **Rich Visualizations**: Feature importance plots, prediction accuracy charts, and error analysis
- **Interactive Interface**: User-friendly command-line interface with step-by-step guidance

## 📊 Performance

Achieves state-of-the-art performance on NASA C-MAPSS datasets:
- **RMSE**: 12-18 cycles (depending on dataset)
- **NASA Score**: Optimized for asymmetric penalty function
- **R²**: 0.75-0.85 correlation with actual RUL values

## 🚀 Quick Start
Download the NASA C-MAPSS dataset from [NASA Prognostics Data Repository](https://ti.arc.nasa.gov/tech/dash/groups/pcoe/prognostic-data-repository/)


### Basic Usage

#### Interactive Mode 
Follow the interactive prompts to:
1. Specify your data directory path
2. Select dataset (FD001-FD004)
3. Choose hyperparameter tuning options
4. View results and visualizations


### Dataset Description
- **FD001**: Single fault mode, single operating condition
- **FD002**: Single fault mode, multiple operating conditions  
- **FD003**: Multiple fault modes, single operating condition
- **FD004**: Multiple fault modes, multiple operating conditions

Each file contains:
- **Training files**: Engine ID, cycle, 3 operational settings, 21 sensor measurements
- **Test files**: Same format as training, but truncated before failure
- **RUL files**: True remaining useful life for each test engine

## 🔧 Advanced Features

### Feature Engineering Pipeline

The system automatically creates 100+ features including:

**Rolling Statistics**
- Moving averages (3, 5, 7 cycle windows)
- Rolling standard deviations
- Trend indicators

**Degradation Indicators**
- Baseline comparisons (first 5 cycles)
- Absolute and relative degradation
- Rate of change features

**Physics-Based Features**
- Temperature ratios (sensor_2/sensor_3, sensor_7/sensor_9)
- Pressure ratios (sensor_4/sensor_11)
- Efficiency indicators (sensor_8 × sensor_13)

**Engine-Level Statistics**
- Per-engine means and standard deviations
- Deviation from engine baseline
- Normalized cycle positions

### Model Architecture

**XGBoost Configuration**
- Gradient boosting with squared error loss
- Automated hyperparameter optimization
- 5-parameter grid search:
  - max_depth: [4, 5, 6]
  - learning_rate: [0.03, 0.05, 0.08, 0.1]
  - n_estimators: [200, 250, 300, 400, 500]
  - subsample: [0.8, 0.85, 0.9]
  - colsample_bytree: [0.8, 0.85, 0.9]

**Regularization**
- L1 regularization (alpha=0.1)
- L2 regularization (lambda=1.0)
- Feature subsampling to prevent overfitting

## 📈 Evaluation Metrics

### Primary Metrics
- **RMSE**: Root Mean Square Error
- **MAE**: Mean Absolute Error  
- **R²**: Coefficient of determination
- **NASA Score**: Asymmetric scoring function penalizing late predictions more heavily


## 📊 Visualizations

The system generates comprehensive visualizations:

1. **Feature Importance Plot**: Top 15 most predictive features
2. **Predictions vs Actual**: Scatter plot with perfect prediction line
3. **Residuals Analysis**: Error distribution and patterns
4. **Performance by RUL Range**: RMSE across different RUL intervals

## 🔬 Technical Details

### Data Preprocessing
- **RUL Capping**: Training RUL values capped at 125 cycles to reduce noise
- **Feature Scaling**: StandardScaler normalization
- **Missing Value Handling**: Mean imputation
- **Infinite Value Treatment**: Replacement with column means

### Validation Strategy
- **Engine-Based Splitting**: 80/20 train/validation split at engine level
- **Prevents Data Leakage**: No engine appears in both training and validation
- **Realistic Evaluation**: Mimics real-world deployment scenario

### Feature Selection
Multi-criteria selection considering:
- **Correlation with RUL**: Pearson correlation coefficient
- **Feature Variability**: Coefficient of variation
- **Mutual Information**: Binned correlation approximation
- **Combined Score**: Weighted combination (40% correlation + 30% CV + 30% MI)

## 📋 Output Files

The system generates several output files:
- `turbofan_results_FD00X.csv`: Detailed predictions per engine
- `feature_importance_FD00X.csv`: Feature importance rankings
- Interactive plots displayed during execution

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

