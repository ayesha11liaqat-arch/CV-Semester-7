# Lab Mid Exam: HOG vs SIFT on Blood-Cell Images

**Course:** Computer Vision Lab
**Name:** Ayesha Liaqat
**Roll No:** FA23-BAI-054
**University:** COMSATS University Islamabad, Wah Campus

## Project Summary

A small lab wants a simple blood-cell classifier that runs on a normal laptop. This project builds two classical computer-vision pipelines and compares how reliable they are when images are **rotated** or **noisy**:

1. **HOG + LinearSVC**
2. **SIFT (fixed grid of keypoints) + LinearSVC**

## Personal Settings (from registration number 054)

| Setting | Rule | My value |
|---|---|---|
| Random seed | Last two digits of reg. no. | **54** |
| HOG cell size | Last digit even: 8 x 8, odd: 16 x 16 | **8 x 8** (4 is even) |
| SIFT grid size | Last digit 0 to 4: 4 x 4, 5 to 9: 6 x 6 | **4 x 4 grid, 16 keypoints** (4 is in 0 to 4) |

## Fixed Settings (same for everyone)

| Item | Value |
|---|---|
| Dataset | BloodMNIST (`medmnist`), size 64 |
| Classes | eosinophil (1), monocyte (5), neutrophil (6), platelet (7) |
| Images per class | 100 train, 30 validation, 30 test (chosen with seed 54) |
| Image preparation | Grayscale, resize to 128 x 128 |
| HOG | 9 orientations, 2 x 2 cells per block |
| Classifier | `LinearSVC`, C chosen from {0.1, 1, 10} on the validation set |
| Rotation test | 20 degrees |
| Noise test | Gaussian noise, sigma = 0.05 (image scaled to 0..1) |

## Repository Contents

| File | Description |
|---|---|
| `FA23-BAI-054_AyeshaLiaqat_LabMid.ipynb` | Executed notebook with all code and outputs (Q1 to Q5) |
| `FA23-BAI-054_AyeshaLiaqat_LabMid.md` | Markdown export of the executed notebook, with outputs visible |
| `FA23-BAI-054_AyeshaLiaqat_LabMid.pdf` | PDF copy of the notebook |
| `README.md` | This file |

## How to Run

1. Open [Google Colab](https://colab.research.google.com) and upload the `.ipynb` file (File, then Upload notebook).
2. Choose **Runtime, then Run all**.
3. The first cell installs `medmnist` and `scikit-image`. BloodMNIST is downloaded automatically by `medmnist`, so no manual download is needed.

Libraries used: `numpy`, `opencv-python` (cv2), `scikit-image`, `scikit-learn`, `pandas`, `matplotlib`, `medmnist`.

## Method Overview

### Q1. Data setup
- Load BloodMNIST (64 x 64), keep the 4 required classes, and sample 100/30/30 images per class using `RandomState(54)`.
- Convert to grayscale and resize to 128 x 128 so every image has the same size and the feature length is fixed.

### Q2. HOG + SVM
- HOG with 8 x 8 cells, 2 x 2 cells per block, 9 orientations, `L2-Hys` block normalisation.
- Feature length by hand: 16 x 16 cells, 15 x 15 blocks, 36 values per block, so 225 x 36 = **8100**.
- `LinearSVC` trained for C in {0.1, 1, 10}; the best C is chosen on the validation set.

### Q3. SIFT + SVM
- Normal `detectAndCompute` gives a different number of keypoints per image, so the feature length changes and an SVM cannot use it.
- Fix: a fixed 4 x 4 grid of keypoints (size 32) over the 128 x 128 image, descriptors computed with `sift.compute` and joined.
- Feature length by hand: 16 grid points x 128 = **2048**.
- Each descriptor is L2-normalised; C is chosen on the validation set.

### Q4. Robustness
- Both models are frozen (not retrained).
- On the **test set**, three cases are evaluated: clean, rotated by 20 degrees, and Gaussian noise (sigma = 0.05).
- The change is applied to the images **before** feature extraction.

### Q5. Short answers and AI log
- Block normalisation, why C must not be chosen on the test set, the most confused classes, and an AI usage log.

## Results

> Fill these tables with the numbers printed in the executed notebook. Do not type numbers that are not in the outputs.

**Validation results (Q2 and Q3)**

| Model | Best C | Validation accuracy | Macro-F1 |
|---|---|---|---|
| HOG + SVM | | | |
| SIFT (grid) + SVM | | | |

**Robustness on the test set (Q4)**

| Model | Clean accuracy | Rotated accuracy | Noisy accuracy |
|---|---|---|---|
| HOG + SVM | | | |
| SIFT + SVM | | | |

## Rules Followed

- Any AI tool was allowed; all code was checked by printing shapes, drawing images and comparing hand calculations with code output.
- The validation set was used to choose C; the test set was touched only in Q4.
- Every number or claim in the answers comes from an output in the notebook.
