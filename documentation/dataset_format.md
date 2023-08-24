# Formatting Your Dataset

To ensure the script and nnUNet run correctly, format your dataset as described below.

## 1. Training Dataset Structure:

Your dataset for training should follow this structure:

\```bash
YOUR_DATASET/
    ├── PATIENT_NUMBER
    │   ├── img.nii.gz
    │   ├── train.nii.gz
\```

Or alternatively:

\```bash
YOUR_DATASET/
    ├── PATIENT_NUMBER
    │   ├── img.nii.gz
    │   ├── validate.nii.gz
\```

Where:
- `PATIENT_NUMBER` is a 4-digit identifier.
- `img.nii.gz` is the naming convention for training images.
- Labels can be named either `train` or `validate`.

## 2. Prediction Dataset Structure:

For prediction, structure your dataset like:

\```bash
YOUR_DATASET/
    ├── PATIENT_NUMBER
    │   ├── test.nii.gz
\```

Ensure you follow this format for optimal performance of the script and nnUNet.
