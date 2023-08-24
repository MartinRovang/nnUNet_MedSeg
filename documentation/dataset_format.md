
# How the have dataset right format


The dataset that user will send into input have to be in a right format oderwise the script will not correctly sort the data and the nnUNet will not correctly run.

First of all, the data set has to be sorted like

```bash
 YOU_DATASET/
    ├── PATIENT_NUMBER
    │   ├── img.nii.gz
    │   ├── train.nii.gz
```

```bash
 YOU_DATASET/
    ├── PATIENT_NUMBER
    │   ├── img.nii.gz
    │   ├── validate.nii.gz
```


```bash
 YOU_DATASET/
    ├── PATIENT_NUMBER
    │   ├── img.nii.gz
    │   ├── test.nii.gz
```
