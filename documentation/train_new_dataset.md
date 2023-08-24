# How to run the python script with new dataset

This scenario will be the most used. Having a trained model on his own dataset is very important fro specific tasks.

# What the user have to do

The user only have to copy its dataset with a specific [format](dataset_format) into the input_nnUNet_train folder and run the exe_train.py.

The script will sort all the data with the right name. all the data using the name 'validate' or 'train' will be included in the training set. 
The code will sorted the data into to 2 folders 'imagesTr' for the images and 'labelsTr' for the filters also a json file will be created with some information that the user has given in the run command line. Those 3 folders are located in the 'raw_nnUnet' folder.
Once the sorted is finished the preprocessing will be made by the nnUNet model. A 2d preprocessing is needed to do the 3d_fullres preprocessing.
The training will be done juste after, using a free gpu. The script will check which GPUs are available and select the first one he find. If no GPU's are available the training is stopped, the data are deleted and the user has try later when one gpu is available. 

When the user run the 'exe_train.py' the time will begin. 
