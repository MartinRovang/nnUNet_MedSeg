# Transfer Learning with nnUNet

Harness the capabilities of an existing model by employing transfer learning.

## Initiating Transfer Learning 

Firstly, ensure your dataset is formatted as described in the [dataset guide](dataset_format.md).

1. **Setup**: Deposit your dataset in the `input_nnUNet_pretrain` directory.
2. **Execution**: Use the following command to kickstart the transfer learning process:

```bash
python3 FULL_PATH/exe_transfer.py -t TIME -f FOLD
```

## Engaging with a Transfer-Learned Model

When tapping into a model refined via transfer learning:

- Merge your new data with the original dataset from the extant model.

Upon running the command, the script:

- Properly locates the data and sets off the preprocessing.
- Segregates the fresh images into their rightful categories, be it training or validation. Cross-check with the specifications in the [training section](training.md#FOLDS).
- Inherits the training blueprint from the antecedent dataset for the current one.
- Initiates the training procedure in line with the specified fold count.
