# Computer Vision Lab 1

## Overview
This repository contains the Jupyter Notebook **`Lab1_CV_054.ipynb`** for a Computer Vision lab exercise. The notebook sets up a Python/PyTorch environment and prepares comparison tables for different machine learning classifiers and model-performance metrics.

## Technologies and Libraries
The notebook uses:

- Python 3
- PyTorch
- Torchvision
- Pandas
- NumPy
- scikit-learn
- XGBoost
- timm
- THOP
- torchinfo

## Installation
Install the required packages using:

```bash
pip install timm thop scikit-learn xgboost torchinfo
```

The notebook also imports PyTorch, Torchvision, Pandas, and NumPy.

## Hardware
The notebook automatically checks whether CUDA is available:

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
```

In the recorded execution, the notebook used the **CPU**.

## Main Components

### 1. Classification Results
The notebook defines a function called `collect_classification_results()` to create a results table for:

- Logistic Regression
- Decision Tree
- Random Forest
- K-Nearest Neighbors
- Linear SVM
- XGBoost

The table contains:

- Accuracy
- Precision
- Recall
- F1-Score
- AUC
- Training Time
- Inference Time

### 2. Additional Model Metrics
The notebook creates a second table containing categories related to:

- Model Size (MB)
- FLOPs (Giga)
- Memory (MB)
- Latency (ms)

### 3. Final Comparison Metrics
A third table is created for:

- Overall Performance
- Robustness
- Scalability
- Energy Efficiency

The table contains performance scores and an error-rate value.

## Important Note
The current notebook uses **randomly generated dummy/placeholder values** for the three result tables. The notebook itself states that these values should be replaced with actual evaluation results from trained models and the specific task requirements.

Therefore, the displayed numerical results should **not be treated as real model-performance measurements**.

## Output
The notebook displays three Pandas DataFrames:

- `df_table1` — classifier comparison
- `df_table2` — model/resource metrics
- `df_table3` — final comparison categories

## How to Run

1. Open `Lab1_CV_054.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab.
2. Select a Python 3 kernel/runtime.
3. Run the dependency-installation cell.
4. Run the remaining cells in order.
5. Review the generated DataFrames.

## Project Structure

```text
.
├── Lab1_CV_054.ipynb
└── README.md
```

## Future Improvements

- Replace dummy values with actual model training and evaluation results.
- Connect the classifiers to a real dataset.
- Calculate the metrics from real predictions.
- Measure actual model size, FLOPs, memory usage, and latency.
- Add visual comparisons such as charts for the evaluation metrics.

## Author
Student ID: **054**
