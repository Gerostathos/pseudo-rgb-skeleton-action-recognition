# Pseudo-RGB Skeleton Action Recognition with CNNs

This project implements a computer vision / deep learning pipeline for **human action recognition** using pseudo-colour image representations of skeletal motion data. The work is inspired by the paper *An Image Representation of Skeletal Data for Action Recognition using Convolutional Neural Networks* and applies CNN-based classification to PKU-MMD pseudo-RGB action images.

The project was developed as part of a Machine Learning assignment and includes experiments on the center camera, all three PKU camera views, cross-view evaluation, data augmentation, k-fold cross-validation, small-dataset training, and transfer learning.

---

## Project Motivation

Instead of using raw RGB video frames, the original method transforms skeletal joint motion into pseudo-coloured images. In this representation, motion information from 3D skeletal trajectories is encoded into image channels, allowing a CNN to classify actions from image-like inputs.

This project explores whether CNN architectures can learn discriminative motion patterns from these pseudo-RGB images and generalize across camera viewpoints and smaller datasets.

---

## Main Features

- Loads pseudo-RGB skeletal action images from the PKU dataset.
- Maps action IDs from filenames to class labels using the provided action-label metadata.
- Filters the selected action classes used in the reference paper.
- Builds a baseline CNN for action classification.
- Implements a configurable CNN for architecture and hyperparameter experimentation.
- Applies train / validation / test splitting.
- Tracks training and validation loss and accuracy.
- Computes confusion matrices, precision, recall, F1-score, and accuracy.
- Performs 5-fold cross-validation.
- Applies image data augmentation.
- Runs single-view and cross-view camera experiments.
- Experiments with a smaller dataset and transfer learning from the PKU-trained model.

---

## Repository Structure

Recommended structure for this GitHub repository:

```text
pseudo-rgb-skeleton-action-recognition/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   └── action_recognition_experiments.ipynb
│
├── src/
│   └── .gitkeep
│
├── reports/
│   └── figures/
│       └── .gitkeep
│
└── data/
    └── README.md
```

The dataset itself should **not** be committed to GitHub if it is large. Keep the `data/` folder local and document where the files should be placed.

---

## Dataset

The experiments use pseudo-RGB action images from the PKU dataset, organized by camera view:

```text
Datasets/
├── PKU/
│   ├── ResActionsImagesM/     # Middle / center camera
│   ├── ResActionsImagesL/     # Left camera
│   ├── ResActionsImagesR/     # Right camera
│   └── PKU_M_CAMERA_TRAIN_TEST_VAL/
│
├── small_dataset/
│   ├── small_dataset_all_files/
│   └── small_dataset_train_test/
│
└── pku_actions_id.xlsx
```

The notebook expects the action ID to be embedded in image filenames, for example:

```text
0312_6856_action_1.csv.png
```

---

## Methods

### 1. Baseline CNN

A custom CNN is trained on the center-camera pseudo-RGB images. The model uses convolutional layers, activation functions, pooling, dropout, and fully connected layers for action classification.

### 2. Configurable CNN

A more flexible CNN implementation allows experimentation with:

- number of convolutional layers,
- channel sizes,
- activation functions,
- dropout,
- optimizer choice,
- learning rate,
- weight decay,
- focal loss.

### 3. Hyperparameter Search

The notebook includes hyperparameter optimization logic to identify stronger model configurations.

### 4. Cross-Validation

A 5-fold cross-validation procedure is implemented to evaluate model stability beyond a single train / validation / test split.

### 5. Data Augmentation

The project tests transformations such as resizing, flipping, rotations, affine transformations, and normalization to improve generalization.

### 6. Cross-View Experiments

The notebook includes experiments for different camera views:

- train and test on the same view,
- train on two views and test on the third view,
- compare center, left, and right camera performance.

### 7. Small Dataset and Transfer Learning

The project also evaluates performance on a smaller dataset, then tests transfer learning by reusing a model trained on PKU data.

---

## Representative Results

These are representative results reported in the notebook runs:

| Experiment | Result |
|---|---:|
| Baseline CNN on center camera | 56.29% test accuracy |
| Optimized center-camera CNN | up to 98.68% test accuracy |
| Center-camera 5-fold cross-validation | 94.94% ± 0.64% |
| Data augmentation on center camera | 94.70% test accuracy |
| Small dataset optimized model | 93.33% test accuracy |
| Small dataset 5-fold cross-validation | 86.67% ± 6.80% |
| Small dataset with augmentation | 86.67% test accuracy |
| Transfer-learning experiment on small dataset | 70.00% test accuracy |

The strongest PKU results come from the optimized configurable CNN, while the smaller dataset experiments show greater variability due to limited data.

---

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/your-username/pseudo-rgb-skeleton-action-recognition.git
cd pseudo-rgb-skeleton-action-recognition
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

```bash
# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add the dataset locally

Place the dataset in:

```text
data/Datasets/
```

Do not commit the full dataset to GitHub.

### 5. Run the notebook

```bash
jupyter notebook notebooks/action_recognition_experiments.ipynb
```

Before running, update any dataset paths in the notebook so they point to your local `data/Datasets/` folder instead of absolute paths from another computer.

---

## Important Implementation Notes

The original assignment instructions mention Keras / TensorFlow, while this implementation is written mainly in **PyTorch**. This should be clearly described as an implementation choice if the repository is used for academic submission. For a job interview portfolio, the PyTorch implementation is still valuable because it demonstrates practical deep learning workflow design, training, evaluation, and experimentation.

The notebook currently contains some hardcoded absolute paths. For a cleaner production-style repository, these should be replaced with relative paths or a configuration file.

Recommended replacement pattern:

```python
from pathlib import Path

PROJECT_ROOT = Path.cwd()
DATA_DIR = PROJECT_ROOT / "data" / "Datasets"
PKU_M_DIR = DATA_DIR / "PKU" / "ResActionsImagesM"
LABELS_PATH = DATA_DIR / "pku_actions_id.xlsx"
```

---

## What This Project Demonstrates

This repository demonstrates:

- deep learning for image-based action recognition,
- PyTorch model implementation,
- CNN architecture design,
- hyperparameter tuning,
- classification metrics and confusion-matrix analysis,
- data augmentation,
- cross-validation,
- transfer learning,
- handling class labels from filenames and metadata,
- experimental comparison across dataset splits and camera views.

---

## Future Improvements

- Refactor the notebook into reusable Python modules under `src/`.
- Add command-line training and evaluation scripts.
- Replace hardcoded paths with a YAML or JSON config file.
- Save metrics automatically into CSV files.
- Add example figures to `reports/figures/` for easier README visualization.
- Add a lightweight inference script for predicting the action class of a single pseudo-RGB image.
