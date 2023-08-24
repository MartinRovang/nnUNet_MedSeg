# Training

The training is a very important part to create a model. 
Using an existing datatset the nnUNet will be trained and the outcome will be a strong medele of 3D segmentation.

To correctly use the nnUNet_medseg programe the user has to follow the direction line to correctly use the program and dont loose any data.

Mainy case are available with this programme
1: train on a completly new data set and generate a new model from scratch (most common)
2: rerun on the same dataset but with other parameters
3: Using a pretrain model


The user will only have interactions with the Input_nnUNet_train, the Input_nnUNet_train and the exe_train.py. 
It is very important that the user has to COPY his dataset in the Input_nnUNet_train because the dataset will be correcly sorted for the nnUNet model and deleted after the operation.
All that the user will have a the end of the training is an output with the trained model. ALL the rest will be DELETED!

To correctly use the exe_train.py here is the command to execute the code: python exe_train.py -d DATASET_NAME -l LABEL -i IMAGE_TYPE -t TIME -f FOLD -e IMAGE_EXTENSION

where DATASET_NAME is the name of the dataset, LABEL is the type of label that the user want to segmente (i.e. TUMOR,...), IMAGE_TYPE is the type of the biomedical images (i.e CT, RMI,...) TIME is the time tha the user wants to train, FOLD is which fold the user want to train, there is maximum 5 fold trainable is the user wants to train all the fold the value has to be "all" this option is highly recommended to have a stong model. Finally the IMAGES_EXTENSION by default is .nii.gz but if the user is using an other extension image he has to write it.

All those parameters have default value and those value will be used if the user forget to fill the parameters lines. 
The epochs number are fixed at 10 000 and the training will stop if it arrives to this number of epochs. Hopefully we added the time to the nnUNet model and the training will be done after the time the user want. The default value of the time is 1 hour of training. Obviously is the time is over in a running epoch, the training will finish the epoch and stop the training just after.
