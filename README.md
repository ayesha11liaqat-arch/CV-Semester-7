# Lab 02 — Effect of Image Filtering on Skin-Lesion Classification

**Student ID:** 054
**Dataset:** HAM10000 (Skin Cancer MNIST)

## Overview
This notebook (`Lab2_CV_054.ipynb`) investigates how five spatial-domain image filters —
Average, Gaussian, Median, Sharpening, and Sobel edge detection — affect the classification
performance of the three best pretrained models identified in Lab Activity 1 (Task 01).

For each of the 3 models, the notebook runs 6 experiments (no filter + 5 filters) using an
identical dataset split, preprocessing pipeline, and training configuration, then compares
results.

## Requirements
```bash
pip install timm scikit-learn torchinfo thop opencv-python torch torchvision pandas numpy matplotlib seaborn
```

## Dataset Setup
1. Download HAM10000 from Kaggle: https://www.kaggle.com/datasets/kmader/skin-cancer-mnist-ham10000
2. Extract it so the folder looks like:
   ```
   HAM10000/
     HAM10000_metadata.csv
     HAM10000_images_part_1/
     HAM10000_images_part_2/
   ```
3. Update `DATA_DIR` in the notebook's configuration cell to point to this folder (defaults to `/content/HAM10000` for Google Colab).

## How to Run
1. Open `Lab2_CV_054.ipynb` in Google Colab (recommended, for GPU) or Jupyter.
2. In the **Configuration** cell, set `BEST_MODELS` to the three models that scored best in your Lab Activity 1 comparison (defaults to `resnet50`, `densenet121`, `efficientnet_b0` as placeholders).
3. Run all cells top to bottom:
   - **Section 1** loads and inspects the dataset, plots class distribution, creates a fixed train/val/test split.
   - **Section 2** defines and visualizes the five filters.
   - **Section 3** defines the dataset/dataloader classes and model loader.
   - **Section 4–5** define training and evaluation functions.
   - **Section 6** is the main experiment loop — trains and evaluates all (model × filter) combinations and saves `lab02_results.csv`.
   - **Section 7** builds the comparison table, delta-vs-baseline table, and summary plots.
   - **Section 8** contains the lab questions with guided answers to fill in from your actual results.
4. Results (metrics table, confusion matrices, training curves, filter examples) are saved as PNG/CSV files alongside the notebook.

## Notes
- `NUM_EPOCHS` is set low (10) by default so a full run completes in a reasonable time; increase it for a more rigorous final result.
- All 18 (model × filter) runs use the same random seed, data split, and hyperparameters for a fair comparison.

## Project Structure
```
Lab02/
├── Lab2_CV_054.ipynb
└── README.md
```
