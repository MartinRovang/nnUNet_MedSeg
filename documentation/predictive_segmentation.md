
# Predictive Segmentation with nnUNet

Using a trained model, it's now possible to make predictions on new images and obtain precise segmentation masks. The process is designed to be user-friendly, minimizing manual intervention.

## Understanding the Prediction Process

After successfully training a model, users should copy the folder named after the dataset from `output_nnUNet_train` to the `model` directory within the prediction set.


The workflow involves placing a ⚠️**COPY**⚠️ of the image they wish to get predictions for into the `input_nnUNet_predict` folder. After the prediction process concludes, the corresponding segmentation masks will be available in the `output_nnUNet_folder` and the input image will be ⚠️**DELETED**⚠️.

## Running the Prediction Script


To start the prediction process with a specific model, use:

```bash
python3 FULL_PATH/exe_predict.py 
```
<details>
  <summary>Click here to have the full named command </summary>
                                                       
```bash
python3 FULL_PATH/exe_predict.py 
```
</details>

The script will automatically use the model located in the `model` directory. nnUNet will then compute an average from various predictions, having previously chosen the best models from the folds. Users can find the resulting image mask they wanted in the `output_nnUNet_prediction` folder.

### Visualizing Results

For those looking to overlay and compare the predicted masks with the original images, the [MedSeg platform](https://www.medseg.ai) is an excellent tool. This can help users verify the accuracy of the segmentation.

