# Predictions

The final aim of having a trained model is to use it on new images and hopefully have perfect masks. The prediction will give to the user mask on his images and completely replace the human intervention.

# How does the prediction works?

The prediction is an easy part of the model. Once the model is trained it will be copied with only the needed folders in the 'model' folder in the predict set. 
The 'input_nnUNet_predict' is made for the user to put his images that he wants to predict. The 'output_nnUNet_folder' will at the end of the process have the mask for the image.


