# Pretraining Using an Existing Model

Leverage the strength of an existing model by fine-tuning it through pretraining. 

## Initiating Pretraining 

Ensure you have a dataset formatted correctly, as per the [dataset guide](dataset_format.md). Place this dataset in the 'input_nnUNet_train' folder. When you execute a specific command, the framework will recognize your intention to pretrain a model.

### Command for Pretraining

```bash
python3 FULL_PATH/exe_train.py PRETRAINING -t TIME 
```

Executing the above will prompt a list of models eligible for pretraining. Simply select your desired model, and the pretraining will initiate with your new data and your specified duration.

**Note**: It's essential that parameters like 'image_type', 'image_extension', and 'labels' align with those of the model you intend to use. This have to be done before the pretraining.

Upon completion, the pretrained model's results will be stored in the 'output_nnUNet_train' directory, replacing any prior models with the newly optimized version.
