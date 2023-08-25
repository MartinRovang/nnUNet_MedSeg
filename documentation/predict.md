
# Predictive Segmentation with nnUNet

Using a trained model, it's now possible to make predictions on new images and obtain precise segmentation masks. The process is designed to be user-friendly, minimizing manual intervention.

## Understanding the Prediction Process

Once a model is successfully trained, only the essential components of that model are transferred to a dedicated `model` directory within the prediction set. 

For users, the workflow involves placing the images they wish to get predictions for into the `input_nnUNet_predict` folder. After the prediction process concludes, the corresponding segmentation masks will be available in the `output_nnUNet_folder`.

## Running the Prediction Script

### 1. Listing Available Models

To get an overview of all models available for predictions, execute the following command:

```bash
python3 PATH/exe_predict.py -l
```

This will display a list of all available models, providing their names for easy reference.

### 2. Running Predictions

To start the prediction process with a specific model, use:

```bash
python3 PATH/exe_predict.py -m MODEL_NAME
```

Replace `MODEL_NAME` with the desired model's name from the list obtained in the previous step.

Once this command is run, the script will process the images in `input_nnUNet_folder` using the selected model. After some time, the `output_nnUNet_predict` directory will have the predicted masks. These masks will retain the original image's name but will append `_predict` to the filename.

### Visualizing Results

For those looking to overlay and compare the predicted masks with the original images, the [MedSeg platform](https://www.medseg.ai) is an excellent tool. This can help users verify the accuracy of the segmentation.

