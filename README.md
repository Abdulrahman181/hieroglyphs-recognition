# Egyptian hieroglyph recognition

This repository contains a TensorFlow transfer-learning notebook for classifying cropped Egyptian hieroglyph images with a ResNet152 ImageNet backbone. **The image dataset is not included.** The saved notebook outputs are not a reproducible model evaluation.

## Data and setup

The notebook expects the dataset root to contain these directories and annotation files:

```text
<dataset-root>/
├── train/_annotations.csv
├── valid/_annotations.csv
└── test/_annotations.csv
```

Each CSV must include `filename`, `xmin`, `ymin`, `xmax`, `ymax`, and `class` columns; the referenced image files must be in the corresponding split directory. The default root is `/kaggle/input/egyptian-hieroglyphs`, suitable for a Kaggle notebook with the matching dataset attached. For a local copy, set `HIEROGLYPHS_DATA_DIR` to the directory containing `train/`, `valid/`, and `test/` before starting the notebook kernel.

Use Python 3.10 or 3.11 and install the declared package ranges:

```bash
python -m pip install -r requirements.txt
```

Open `egyptian-hieroglyphs-using-tl-cnn.ipynb` in Jupyter or Kaggle and run cells in order. A working internet connection may be needed for Keras to retrieve pretrained ImageNet weights. The notebook loads split images into memory, so available RAM/GPU capacity constrains the dataset size.

## Correctness notes

The class encoder is fitted only on training labels and reused for validation and test labels. Splits containing a class absent from training now fail explicitly rather than silently assigning incompatible one-hot indices. The model output width is derived from the training classes instead of assuming 95 classes. The prior saved training/evaluation outputs were cleared because they were produced with independently fitted encoders and do not validate the corrected pipeline; retained data-preview images are merely prior notebook output.

## Validation and limitations

The repository does not contain the dataset, and no training run or model-performance claim is provided here. Dependency ranges are an intended compatibility baseline, not a lockfile or proof that every platform has been tested. After attaching the expected dataset, run the notebook from top to bottom and verify its validation/test metrics in your environment.
