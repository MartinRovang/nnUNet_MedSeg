# Pretraining with an Existing Model

Optimize your results by fine-tuning an existing model through pretraining.

## Starting the Pretraining 

Before initiating, ensure your dataset aligns with the format outlined in the [dataset guide](dataset_format.md).

1. **Setup**: Place your dataset into the `input_nnUNet_pretrain` directory.
2. **Execution**: Run the command below to begin the pretraining process:

```bash
python3 FULL_PATH/exe_pretrain.py -t TIME -f FOLD
```

## Working with a Pretrained Model
When leveraging a pretrained model:

- Use a dataset merging both the original data (from the existing model) and your new contributions.

On command execution, the script:

- Places data in appropriate folders and initiates preprocessing.
- Sorts the new images in their respective categories: either training or validation. Ensure they align with the format in the [training section](training.md#FOLDS).
- Shares the same training plan from the previous dataset for the new one.
- Begin the training based on the desired number of folds. 
