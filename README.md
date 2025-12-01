# Time-Series-Forecasting-for-Transformer-Fault-Diagnosis
A comprehensive GUI-based tool for predicting gas concentrations in power transformers using state-of-the-art deep learning architectures. Designed for dissolved gas analysis (DGA) in transformer maintenance with support for multiple forecasting models, robust validation techniques, and user-friendly workflows.
Purpose
This tool enables electrical engineers and maintenance personnel to forecast future gas concentrations (H₂, CH₄, C₂H₆, C₂H₄, C₂H₂) in power transformers without requiring machine learning expertise. By analyzing historical DGA data, the system provides early warnings of potential transformer faults through predictive modeling.
Key Features
Multiple Model Architectures

DLinear: Fast, lightweight model ideal for linear trends and quick predictions
PatchTST: Patch-based transformer with superior performance on complex patterns
LSTM-Paper: Implementation from Hu et al. (2020) optimized for 5-gas prediction
TimesNet: Advanced architecture for data with multiple periodic patterns

Robust Validation Options

Train/Test Split: Traditional 80/20 temporal split for quick model evaluation
K-Fold Cross-Validation: TimeSeriesSplit with customizable folds (2-10) for robust performance metrics
Full Training Mode: Train on all available data for maximum prediction accuracy

Intelligent Data Handling

Automatic Frequency Detection: Supports daily, weekly, monthly, bimonthly, and yearly data
Adaptive Parameter Settings: Automatically adjusts sequence and prediction lengths based on data frequency
Missing Value Handling: Built-in interpolation and preprocessing for incomplete datasets
Smart Scaling: Per-gas normalization with log transforms for high-variance gases like H₂

Advanced Forecasting Capabilities

Historical Predictions: Generate predictions for existing data to validate model performance
Future Forecasting: Extend predictions beyond available data (user-configurable horizon)
Flexible Output Frequency: Choose different prediction intervals (e.g., train on monthly, predict daily)
Multi-Gas Support: Predict all 5 gases simultaneously or focus on individual gases

Comprehensive Analysis Tools

Error Metrics Dashboard: MAE, RMSE, and R² scores with visual scatter plots
Excel Export: Detailed error trends and performance metrics in organized spreadsheets
Interactive Plotting: Visualize actual vs. predicted values with future forecasts highlighted
Model Persistence: Save and reload trained models for reuse on new data

Workflow

Load Data: Import Excel file with timestamp and gas concentration columns
Configure Model: Select architecture, gas type, and training parameters
Train: Use traditional split or K-fold cross-validation for robust training
Predict: Generate forecasts for historical validation and future periods
Analyze: Review error metrics, visualize results, and export predictions
Deploy: Save trained models for continuous monitoring on new data

Technical Specifications

Framework: PyTorch-based neural networks with GPU acceleration support
Data Processing: Pandas, NumPy, scikit-learn for preprocessing and scaling
Validation: TimeSeriesSplit for temporal integrity in cross-validation
GUI: Tkinter with matplotlib integration for interactive visualization
Export Formats: Excel (.xlsx) for predictions and PNG/PDF for plots

Use Cases

Preventive Maintenance: Forecast gas concentrations to schedule maintenance before failures
Fault Detection: Identify abnormal trends indicating incipient transformer faults
Asset Management: Compare predictions across transformer fleets for prioritization
Research: Benchmark different forecasting architectures on DGA data
Training: Educate personnel on transformer health monitoring with visual tools

Getting Started
Prerequisites
bashpip install torch pandas numpy scikit-learn matplotlib openpyxl
Basic Usage
bashpython gui_tool.py
```

1. Click **Browse** → Select your Excel file with DGA data
2. Click **Load** → Tool auto-detects frequency and suggests parameters
3. Select **Model** (DLinear recommended for beginners)
4. Choose **Gas** (All gases or individual selection)
5. Click **Train** → Monitor progress in status log
6. Click **Predict** → Generate forecasts
7. Click **Plot** → Visualize results
8. Click **Save Results** → Export to Excel

### Advanced Features

**K-Fold Cross-Validation:**
1. Enable "K-Fold CV" checkbox
2. Set K value (5-10 recommended)
3. Train → System tests model on multiple time periods
4. Best model automatically selected and retrained on all data

**Model Reuse:**
1. After training, click **Save Model**
2. Later: Go to "Load Model" tab → Browse for .pth file
3. Skip training → Directly predict on new data

**Error Analysis:**
1. After predictions, go to "Error Analysis" tab
2. Click **Calculate Error Metrics**
3. View scatter plots and performance statistics
4. Click **Export Error Metrics to Excel** for detailed reports

## Data Format Requirements

Your Excel file should contain:
- **Timestamp column**: Named "Timestamp", "Date", or "DateTime"
- **Gas columns**: H2, CH4, C2H6, C2H4, C2H2 (any or all)
- **Chronological order**: Data sorted by time (tool will sort if needed)
- **Minimum samples**: At least 50 data points recommended for monthly data

## Model Selection Guide

| Model | Best For | Speed | Accuracy | Complexity |
|-------|----------|-------|----------|------------|
| DLinear | Linear trends, stable data | Fast | Good | Low |
| PatchTST | Complex patterns, long sequences | Medium | Excellent | Medium |
| LSTM-Paper | 5-gas joint prediction | Medium | Very Good | Medium |
| TimesNet | Multi-periodic patterns | Slow | Excellent | High |

## Output Files

- **Predictions Excel**: Timestamp, Actual values, Predicted values, Future forecasts
- **Error Metrics Excel**: MAE/RMSE/MAPE/R² summary + detailed error trends per timestamp
- **Model Files (.pth)**: Saved models with configuration for reuse
- **Plots (PNG/PDF)**: Publication-ready visualizations with actual/predicted/future series

## Research Background

This tool implements methodologies from transformer fault diagnosis research, integrating:
- Dissolved Gas Analysis (DGA) interpretation standards
- Time series forecasting with deep learning
- Confidence scoring frameworks for diagnostic reliability
- Practical deployment considerations for field engineers

Developed as part of UREP (Undergraduate Research Experience Program) and URS (Undergraduate Research Scholars) at TAMUQ focusing on proactive transformer maintenance through machine learning-based gas concentration forecasting.

## Citation

If you use this tool in your research, please cite:
```
[IEEE paper citation]
🛠️ Troubleshooting
"No predictions" or "Flat predictions":

Try PatchTST instead of DLinear
Increase epochs (100 → 200)
Check if data has sufficient variation

"Training loss high":

Enable K-Fold CV for better generalization
Verify data quality (remove outliers manually)
Try log transformation for high-variance gases

"Future predictions unrealistic":

Reduce future_periods (forecasts degrade beyond 6 months for monthly data)
Use K-Fold to ensure model reliability
Check if training data covers similar patterns

Support
For questions, issues, or contributions, please open an issue on GitHub or contact [amsinno06@gmail.com].
License
[MIT]
 
