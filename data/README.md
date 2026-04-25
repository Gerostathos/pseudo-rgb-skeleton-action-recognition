# Dataset Instructions

This folder is reserved for the dataset used by this project.

The actual dataset files are **not committed to GitHub**. To run the project locally, place the prepared pseudo-RGB skeleton action-recognition dataset inside this folder using the structure shown below.

This repository does **not** contain the full PKU-MMD dataset or the processed assignment dataset files. The local folders used by this project appear to be a prepared/processed dataset representation derived from PKU-MMD skeletal data, rather than the raw official PKU-MMD download.

## Dataset Source

The original PKU-MMD dataset can be found from the official PKU-MMD project page:

```text
https://struct002.github.io/PKUMMD/
```

PKU-MMD is a multi-modal human action dataset that provides resources such as RGB videos/images, depth maps, infrared sequences, and skeleton joint data. This project uses the skeleton-based / pseudo-RGB image representation prepared for the assignment, not the full raw multi-modal dataset directly.

## Expected Local Structure

After obtaining the prepared dataset files, place them locally using the following structure:

```text
data/
└── Datasets/
    ├── PKU/
    │   ├── ResActionsImagesM/
    │   ├── ResActionsImagesL/
    │   ├── ResActionsImagesR/
    │   └── PKU_M_CAMERA_TRAIN_TEST_VAL/
    │
    ├── small_dataset/
    │   ├── small_dataset_all_files/
    │   └── small_dataset_train_test/
    │
    └── pku_actions_id.xlsx
```

## Expected Path

When running the notebooks, the code expects the dataset to be available under:

```text
data/Datasets/
```

The notebooks use the prepared pseudo-RGB action images and related train/test split files from this local dataset directory.

## Important Clarification

The folder structure above is the structure expected by this project and by the provided notebooks. It should not be assumed that these exact folders can be downloaded directly from the official PKU-MMD page.

The official PKU-MMD source provides the original dataset resources. This project expects a processed assignment dataset containing pseudo-RGB skeleton action image folders and helper files.

## Notes

- The dataset files are intentionally excluded from this repository to keep the GitHub project lightweight.
- The dataset may contain coursework-provided files or processed files derived from third-party data, so it should not be redistributed unless the license explicitly allows it.
- Only this `README.md` file should be committed inside the `data/` folder.
- If your local folder names differ, either update the notebook paths or rename the folders to match the expected structure above.
