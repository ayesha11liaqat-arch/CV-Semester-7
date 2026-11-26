# CNN Feature Visualization, Parameter Audit & Critical Analysis

This project implements the **Deep Learning & Computer Vision practical
lab assignment**. It demonstrates how five custom 3×3 filters transform
an image through convolution, ReLU activation, max pooling, and average
pooling. It also builds and compares two small CNN architectures using
TensorFlow/Keras.

## 1. Project contents

``` text
CNN_Lab/
│
├── cnn_lab_assignment.py
├── input.jpg
├── README.md
├── CNN_Visualization.png       # Generated after running the script
└── screenshots/
    ├── model_a_summary.png     # Capture from the terminal
    └── model_b_summary.png     # Capture from the terminal
```

## 2. Requirements

-   Python 3.9 or newer
-   VS Code, PyCharm, or another Python IDE
-   An input image named **`input.jpg`**
-   Internet connection for installing the required packages

## 3. Install required libraries

Open a terminal in the project folder and run:

``` bash
pip install numpy matplotlib opencv-python tensorflow
```

If your computer uses the `python3` command, use:

``` bash
python3 -m pip install numpy matplotlib opencv-python tensorflow
```

## 4. Prepare the input image

1.  Select a clear image containing visible horizontal and vertical
    edges, textures, and contrast.
2.  Copy the image into the same folder as `cnn_lab_assignment.py`.
3.  Rename it exactly to `input.jpg`.

The code reads the image, converts it to grayscale, and resizes it to
256 × 256 pixels.

## 5. Run the implementation

Open the project folder in your IDE. In the terminal, run:

``` bash
python cnn_lab_assignment.py
```

The program will:

1.  Read and preprocess `input.jpg`.
2.  Define five custom 3×3 kernels.
3.  Apply each kernel independently using convolution.
4.  Apply ReLU to each raw feature map.
5.  Apply 2×2 max pooling with stride 2 to the ReLU output.
6.  Apply 2×2 average pooling with stride 2 to the ReLU output.
7.  Display and save the 5 × 4 visualization grid.
8.  Build Model A and Model B.
9.  Print both Keras model summaries and parameter totals.

## 6. Five filters used

  -----------------------------------------------------------------------
  Filter                              Purpose
  ----------------------------------- -----------------------------------
  Horizontal Edge (Sobel-X)           Detects intensity changes in the
                                      horizontal direction; highlights
                                      vertical edge lines.

  Vertical Edge (Sobel-Y)             Detects intensity changes in the
                                      vertical direction; highlights
                                      horizontal edge lines.

  Sharpen                             Enhances details and edges.

  Box Blur                            Smooths the image by averaging
                                      neighboring pixels.

  Emboss                              Produces a directional
                                      raised/recessed appearance.
  -----------------------------------------------------------------------

## 7. Four processing stages

  -----------------------------------------------------------------------
  Stage                   Operation               Description
  ----------------------- ----------------------- -----------------------
  A                       Raw Convolution         Direct filter response
                                                  before activation.

  B                       ReLU                    Replaces negative
                                                  values with zero:
                                                  `max(0, x)`.

  C                       Max Pooling             Takes the maximum value
                                                  from each 2×2 region,
                                                  stride 2.

  D                       Average Pooling         Takes the mean value
                                                  from each 2×2 region,
                                                  stride 2.
  -----------------------------------------------------------------------

Both pooling operations are applied to the **post-ReLU feature map**, as
specified in the assignment.

## 8. CNN model architectures

Both models accept RGB input images of size 32 × 32 × 3 and use two
convolution layers, one pooling layer, Global Average Pooling, and a
10-class Dense output.

  Configuration                         Model A           Model B
  ------------------------------- ------------- -----------------
  Conv1 filters                               5                 5
  Conv2 filters                              10                10
  Kernel size                             3 × 3             5 × 5
  Pooling                           Max Pooling   Average Pooling
  Pool size / stride                  2 × 2 / 2         2 × 2 / 2
  Output classes                             10                10
  Expected trainable parameters         **710**         **1,750**

The models use `padding="same"` and ReLU activations after both
convolution layers. These are implementation choices because the
assignment does not specify padding or convolution activations.

### Parameter formula

For each convolution layer:

``` text
(Kh × Kw × Cin + 1) × Cout
```

The extra 1 represents one bias for each output filter.

**Model A**

``` text
Conv1 = (3 × 3 × 3 + 1) × 5 = 140
Conv2 = (3 × 3 × 5 + 1) × 10 = 460
Dense = (10 × 10) + 10 = 110
Total = 140 + 460 + 110 = 710
```

**Model B**

``` text
Conv1 = (5 × 5 × 3 + 1) × 5 = 380
Conv2 = (5 × 5 × 5 + 1) × 10 = 1,260
Dense = (10 × 10) + 10 = 110
Total = 380 + 1,260 + 110 = 1,750
```

Global Average Pooling has no trainable parameters.

Percentage increase from Model A to Model B:

``` text
((1750 - 710) / 710) × 100 = 146.48%
```

## 9. Expected output files and evidence

After a successful run, the program saves:

-   `CNN_Visualization.png` --- the 5 × 4 grid of filters and processing
    stages.

The model summaries are printed in the terminal. Capture screenshots
of: - Model A summary - Model B summary

Include these screenshots and the generated visualization in your
assignment submission.

## 10. Troubleshooting

### `input.jpg not found`

Make sure the image is in the same folder as the Python script and its
name is exactly `input.jpg`.

### `ModuleNotFoundError`

Install the missing package using:

``` bash
pip install numpy matplotlib opencv-python tensorflow
```

### TensorFlow installation or compatibility error

Check your Python version and install a TensorFlow version compatible
with your operating system and Python environment. If you use a virtual
environment, activate it before installing packages and running the
script.

### Visualization window does not appear

The image is also saved as `CNN_Visualization.png` in the project
folder. Open that file to inspect the result.

## 11. Assignment checklist

-   [ ] Five custom 3×3 filters implemented.
-   [ ] Raw convolution output generated for every filter.
-   [ ] ReLU activation applied.
-   [ ] Max pooling (2×2, stride 2) applied.
-   [ ] Average pooling (2×2, stride 2) applied.
-   [ ] 5 × 4 visualization generated and saved.
-   [ ] Model A implemented and summary captured.
-   [ ] Model B implemented and summary captured.
-   [ ] Manual parameter calculations included.
-   [ ] Answers to all five critical-thinking questions prepared.

------------------------------------------------------------------------

**Note:** Run the code on your own computer and verify the generated
visualization and model summaries before submitting. The script does not
train the models; it builds them and reports their architecture and
parameter counts, as required for the architecture comparison.
