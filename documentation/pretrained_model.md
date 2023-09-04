# Pretraining with an Existing Model

Optimize your results by fine-tuning an existing model through pretraining.

## Starting the Pretraining 

Before initiating, ensure your dataset aligns with the format outlined in the [dataset guide](dataset_format.md).

1. **Setup**: Place your dataset into the `input_nnUNet_pretrain` directory.
2. **Execution**: Run the command below to begin the pretraining process:

```bash
python3 FULL_PATH/exe_pretrain.py -t TIME 
```

## Working with a Pretrained Model
When leveraging a pretrained model:

Use a dataset merging both the original data (from the existing model) and your new contributions.
On command execution, the script:
Places data in appropriate folders and initiates preprocessing.
Modifies the splits_final JSON file, defining different folds (balances of training to validation). This ensures data consistency and quality, with new data being added and sorted appropriately.
Training proceeds using the adjusted split and the weights from the model being fine-tuned. Like initial training, each fold trains individually, leading to 5 distinct models—one per fold.
