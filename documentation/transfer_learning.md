# Transfer Learning with nnUNet

Leverage the power of an existing model through the application of transfer learning. 
**Exemple of use**: Imagine a scenario where a user has trained a model in one hospital using a specific dataset, and now wishes to utilize this model in a different hospital. Instead of training an entirely new model from scratch, transfer learning allows the existing model to be updated and enhanced with new data from the new hospital.

## Initiating Transfer Learning 

Firstly, ensure your dataset is formatted as described in the [dataset guide](dataset_format.md).

1. **Setup**: Deposit your dataset in the `input_transferLearning` directory.
2. **Model**: Don't forget to copy paste the model you want to fine tune in the `model` folder from the `output_model` folder in the train one.
3. **Execution**: Use the following command to kickstart the transfer learning process:

```bash
python3 FULL_PATH/exe_transferLearning.py -t TIME 
```

## Engaging with a Transfer-Learned Model

When tapping into a model refined via transfer learning:

- Merge your new data with the original dataset from the existing model.
- Or use completely new data

Upon running the command, the script:

- Properly locates the data and sets off the preprocessing.
- Splits the new images into their rightful categories, be it training or validation. Cross-check with the specifications in the [training section](training.md#FOLDS).
- Uses the same plans as the previous dataset to have the same topology.
- As the training, the user will have in the `output_transferLearning` the fine tuned model.
  
