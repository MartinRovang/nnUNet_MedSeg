# Welcome to the nnUNet_MedSeg 

This script will help people to use the [nnUNetv2](https://github.com/MIC-DKFZ/nnUNet) model more easily. 

# What is this script made for? 

The script easily implement the nnUNetv2 model used to do segmentation of biomedical images.
The script is made to help people using the model without implementing it and understand it. 
The only thing that people have to do is to have a dataset with a certain name of folder and copy the dataset in the input folders of the script.

# How does the script works?

The script is made of 3 different files. The train, the predict and the docker image.

Once the user put a COPY of his dataset in the Input_nnUNet_train, it only has to run the exe_train.py to have an output file.
The user can also do a prediction with the model. Once the training is done the user has to COPY a test dataset and drop it in the Input_nnUNet_predict folder to have prediction images.

# train folder

The train folder is composed by different folders that the nnUNet need to correclty run. All the different subfolders are listed in the image below
The user will only have interactions with the Input_nnUNet_train, the Input_nnUNet_train and the exe_train.py. 
It is very important that the user has to COPY his dataset in the Input_nnUNet_train because the dataset will be correcly sorted for the nnUNet model and deleted after the operation. 


# predict folder

The predict folder looks like the train folder. The 



# docker image folder

A docker image have been made the correctly regroupe different software that the script needs. There is Pytorch version 2.0.0, CUDA version 11.8 and the nnUNet model.
The docker image will be loaded on the user hardware and will be used to do all the process.







<img src="pictures/folders_train_predictV2.drawio%20(1).png" width="500"  />

Please cite the [following paper](https://www.google.com/url?q=https://www.nature.com/articles/s41592-020-01008-z&sa=D&source=docs&ust=1677235958581755&usg=AOvVaw3dWL0SrITLhCJUBiNIHCQO) when using nnU-Net:

    Isensee, F., Jaeger, P. F., Kohl, S. A., Petersen, J., & Maier-Hein, K. H. (2021). nnU-Net: a self-configuring 
    method for deep learning-based biomedical image segmentation. Nature methods, 18(2), 203-211.

