# Use an existing model for pretraining

The pretraining is very usefull if the user wants to fine tune an existing model.

# How to pretrain a model?

If the user put a well  [formated](dataset_format.md) dataset file in the 'input_nnUNet_train' folder and execute a special command, the script will automatically detect that the user wants ton pretrain a model. 
Command to execute the pretraining:

'''bash
python3 PATH/exe_train.py PRETRAINING -t TIME 
'''
With this command, the script will send to the user a list of all the different models that are able to be used for the pretraining.
The user will juste choose the one that he wants and the pretraining will begin with the new data and the time choosed by the user. 

Obviously, the different parameters like the 'image_type', 'image_extension', 'labels' (cf [see on the ](train_new_dataset) have to be the same as the trained model that the user will use.
