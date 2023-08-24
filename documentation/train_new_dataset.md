#How to run the python script with new dataset

This scenario will be the most used. Having a trained model on his own dataset is very important fro specific tasks.

#What the user have to do

The user only have to copy its dataset with a specific format into the input_nnUNet_train folder and run the exe_train.py.

The script will sort all the data with the right name. all the data using the name 'validate' or 'train' will be included in the training set. 
The code will sorted the data into to 2 folders 'imagesTr' for the images and 'labelsTr' for the filters. Those 2 folders are located in the 'raw_nnUnet' folder.
Once 
