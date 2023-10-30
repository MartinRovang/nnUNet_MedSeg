## Documentation for `generalFunctions.py`

---

### Overview

The `generalFunctions.py` script is designed to contains all the functions that are general for both scripts (mainly train and transfer learning)

### Table of Contents

- [Prerequisites](#prerequisites)
- [Functions](#functions)


---

### Prerequisites

Ensure you have the following libraries installed:

- os
- json
- sys
- shutil
- subprocess
- datetime import datetime
- time as tm
- eSimpleITK as sitk
- delete_all (python script)
- globalPath (python script)


---

### Main execution

At first, some global variables and paths are defined to ensure the code to work correctly. After that, all the necessary functions to preprocess and process for the training/transfer learning are defined as well.

<details>
  <summary><strong>Click to view the code for the code for the main execution</strong></summary>

```python
"""-----------------------------GLOBAL VARIABLES------------------------------"""
#GLOBAL VARIABLES
full_dataset_name = ""
container_id = ""
fold_all_value = False
file_ending = ".nii.gz"
image_docker = "nnunet_timev22"
current_script = None
image_type = None
time_input = None

#TRAINING VARIABLES
timer_training_start = None
dataset_name = None
label_number = None
configuration_model = None


#TRANSFER LEARNING VARIABLES
part_tot=[]
new_data=[]
new_data_train=[]
new_data_val = []
name_img_dic = {}
timer_pretraining_start = None
fold_0_or_all_value = None
fold_cross_validation_number = 5
split_final_json = "splits_final.json"
dataset_source_name = "Dataset999_SOURCE"


#MAIN PATHS 
main_path = os.path.dirname(os.path.abspath(__file__)) #Get the parent path of the main folder
```

</details>


---

### Functions
:point_right: **Start_process_training(timer_training_start_fct, dataset_name_fct, label_number_fct, image_type_fct, time_input_fct, configuration_model_fct)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Set up the correct values and launch the process for the training
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `timer_training_start_fct` (int): It is the value of the timer to know how much time the code takes for the process
  - `dataset_name_fct` (str): Name of the model
  - `label_number_fct` (int): Number of label that is in the process
  - `image_type_fct` (str): Type of the image (CT, MRI,..)
  - `time_input_fct` (int): Time for the training
  - `configuration_model_fct` (str): Configuration of the model (3d_fullred, ...)
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Start_process_training`</strong></summary>

```python
# Code for the function check_for_train_or_validate
def start_process_training(timer_training_start_fct, dataset_name_fct, label_number_fct, image_type_fct, time_input_fct, configuration_model_fct):
    global timer_training_start, dataset_name, label_number, image_type, time_input, configuration_model, current_script

    #Setting up the different variables
    current_script = "train"
    timer_training_start = timer_training_start_fct
    dataset_name = dataset_name_fct
    label_number = label_number_fct
    image_type = image_type_fct
    time_input = time_input_fct
    configuration_model = configuration_model_fct

    #Setting up the correct paths
    globalPath.myPath(current_script)

    #Starting the actual process
    create_structure(train=True)
```
</details>


##


:point_right: **Start_process_tl(timer_pretraining_start_fct, label_number_fct, image_type_fct, time_input_fct, configuration_model_fct)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Set up the correct values and launch the process for the transfer learning
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `timer_pretraining_start_fct` (int): It is the value of the timer to know how much time the code takes for the process
  - `label_number_fct` (int): Number of label that is in the process
  - `image_type_fct` (str): Type of the image (CT, MRI,..)
  - `time_input_fct` (int): Time for the training
  - `configuration_model_fct` (str): Configuration of the model (3d_fullred, ...)
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Start_process_tl`</strong></summary>

```python
# Code for the function check_for_train_or_validate
def start_process_tl(timer_pretraining_start_fct, label_number_fct, image_type_fct, time_input_fct, configuration_model_fct):
    global timer_pretraining_start, label_number, image_type, time_input, configuration_model, current_script, fold_0_or_all_value

    #Setting up the correct paths
    current_script = "transferLearning"
    globalPath.myPath(current_script)
    delete_all.clean_all(delete_input_folder=False, delete_output_folder=True, delete_model_folder=False, delete_all_nnunet_folder=False, script=current_script)
    get_model_name()

    #Setting up the different variables
    timer_pretraining_start = timer_pretraining_start_fct
    label_number = label_number_fct
    image_type = image_type_fct
    time_input = time_input_fct
    configuration_model = configuration_model_fct

    
    
    fold_0_or_all_value = get_fold_value()

    #Starting the actual process
    create_structure(train=False)
```
</details>


##


:point_right: **Get_model_name( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Get the model name 
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - : path to the `model` folder.
- ![Returns](https://img.shields.io/badge/-Returns-red)
   -`full_dataset_name` (str): name of the dataset/model

<details>
  <summary>Click to view the code for the function `Get_model_name( )`</summary>

```python
# Code for the function get_model_name
def get_model_name():
    global full_dataset_name

    for folder in os.listdir(globalPath.model_folder_path):
        if full_dataset_name == "":
            full_dataset_name = folder
        else:
            print("2 differents model, keep only 1!")
            delete_all.clean_all(delete_input_folder=True, delete_output_folder=True, delete_model_folder=True, delete_all_nnunet_folder=True, script=current_script)
            sys.exit()
```

</details>


##


:point_right: **Get_fold_value( )** :point_left:
- ![Purpose](https://img.shields.io/badge/-Purpose-green) Check the fold value.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) return the folder value
<details>
  <summary>Click to view the code for the function `Get_fold_value( )`</summary>
  
```python
# Code for the function get_fold_value
def get_fold_value():
  for folder in os.listdir(os.path.join(globalPath.model_folder_path, full_dataset_name, "nnUNetTrainer__nnUNetPlans__3d_fullres")): #Change here if you are changing the configuration of the model!
      if folder.split("_")[0] == "fold":
          return folder.split("_")[1] 
```
</details>


##


:point_right: **Create_structure(train)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates the main folder directory (with the right name) + all the necessary json files
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
 - `train` (Boolean): True or false. To know in which case we are.
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Create_structure( )`</strong></summary>

```python
def create_structure(train):
    global full_dataset_name, fold_all_value

    if train:
        next_number = 1 
        main_folder_name = f"Dataset{next_number:03}_{dataset_name}"  #Formatting the number to be 3 digits
        full_dataset_name = main_folder_name

    main_folder_path = os.path.join(globalPath.nnunet_raw_path , full_dataset_name)  # Combine with actual_path (nnunet raw folder)

    if not os.path.exists(main_folder_path): #Check if the name already exists (normally not because everything is deleted after each training)
        os.makedirs(main_folder_path)
    else:
        print(f"Folder {full_dataset_name} already exists.")
        return

    #Create 2 sub-folders inside the main folder
    subfolders = ['imagesTr', 'labelsTr']
    for subfolder in subfolders:
        os.makedirs(os.path.join(main_folder_path, subfolder))

    #Definition of paths and variables
    img_destination = os.path.join(globalPath.nnunet_raw_path, full_dataset_name, "imagesTr") 
    train_destination = os.path.join(globalPath.nnunet_raw_path, full_dataset_name, "labelsTr")
    num_training = 0
    num_images = 0
    tr_cases = 0
    val_cases = 0
    train_img_list = []
    validate_img_list=[]

    #Moving the images in the right directory
    for directory in os.listdir(globalPath.input_folder_path): #For loop on the input folder (there should be only 1 folder inside!)
        directory_path = os.path.join(globalPath.input_folder_path, directory)

        for img_directory in os.listdir(directory_path): #For loop on all the folder inside the folder input
            img_directory_path = os.path.join(directory_path, img_directory)

            for files in os.listdir(img_directory_path): #For loop on all the folder to get the img and mask niifti image      
                if check_for_train_or_validate(img_directory_path): #Returns True if the name starts with train or validate, otherwise, returns False and we don't use this image for the training
                    file_path = os.path.join(img_directory_path, files)
                    first_name = files.split('.')[0]
                    new_filename = img_directory  #Rename file with folder name prepended (Patient number)
                                    
                    # Check the file's prefix and move accordingly
                    if first_name == 'img': 
                        num_images += 1
                        new_name_img = new_filename +  '_' + '0000' + '.' + 'nii' + '.' + 'gz' #Rename the image correctly
                        shutil.copy2(file_path, os.path.join(img_destination, new_name_img))
                                        
                    elif first_name == 'train' or first_name == 'validate':
                        num_training += 1
                        new_name_img = new_filename + '.' + 'nii' + '.' + 'gz' #Rename the mask correctly
                        process_image(file_path, os.path.join(train_destination, new_name_img)) #This function allows us to keep only the number of labels wanted for the training
                        if first_name == "train": #This will allow us to create a json file to keep track of which image were used for the training and for the validation (uuseful for transfer learning)
                            tr_cases += 1
                            train_img_list.append(new_filename)
                        elif first_name == "validate":
                            val_cases += 1
                            validate_img_list.append(new_filename)

    if len(validate_img_list) == 0: #If there is none validitate image, we do the fold all (all images are used both in the validation and training)! 
        fold_all_value = True


    #Check if the number of images is normal                 
    if num_training == num_images:

        create_split_json(train_img_list, validate_img_list, current_script) #Split json is created to use the right image in the training and in the validation 

        # Create a dataset JSON file inside the main folder to be able to start the nnUNet model training
        channel_names = get_channel_names() # Get channel names
        labels = get_labels() # Get labels
        json_file_path = os.path.join(main_folder_path, 'dataset.json')
        with open(json_file_path, 'w') as json_file:
            data = {
                "channel_names": channel_names,
                "labels": labels,
                "numTraining": num_training,
                "file_ending": file_ending
            }
            json.dump(data, json_file, indent=4)

        #Create a JSON file info to have some information of the model
        json_file_path = os.path.join(globalPath.dataset_train_path, 'info_model.json')
        data = {
            "training cases": tr_cases,
            "validation cases": val_cases,
            "creation date": datetime.now().strftime("%Y-%m-%d %H:%M:%S") ,
            "total time": time_input,
        }
        with open(json_file_path, 'w') as json_file:
            json.dump(data, json_file, indent=4)

        print("Files moved and renamed successfully!")
        print(f"Successfully created structure in {main_folder_path}")

        #Delete the input directory to clean up the input folder
        for directory in os.listdir(globalPath.input_folder_path): 
            directory_path = os.path.join(globalPath.input_folder_path, directory)
            shutil.rmtree(directory_path)
            print(f"Input folder ({directory}) has been deleted")

        launch_docker(full_dataset_name, current_script) #Once the images are well separated, the training can start
```

</details>


##


:point_right: **Check_for_train_or_validate(directory)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Determines if the provided directory contains images designated for training or validation.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `directory` (str): Path to the directory to check.
- ![Returns](https://img.shields.io/badge/-Returns-red): 
  - `True` if training or validation images are found.
  - `False` otherwise.

<details>
  <summary><strong>Click to view the code for the function `check_for_train_or_validate`</strong></summary>

```python
# Code for the function check_for_train_or_validate
def check_for_train_or_validate(directory):
    for filename in os.listdir(directory): #List all the files in the folder
        if filename.startswith('train.') or filename.startswith('validate.'): #Check if the name starts with "train" or "validate"
            return True
    return False
```

</details>


##


:point_right: **Process_image(input_filename_path, output_filename_path)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Processes a NIfTI image to retain only a specified label.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `input_filename_path` (str): Path to the input image.
  - `output_filename_path` (str): Path to save the processed image.
- ![Returns](https://img.shields.io/badge/-Returns-red):
 - The processed image are saved to the specified path.

<details>
  <summary><strong>Click to view the code for the function `Process_image(input_filename_path, output_filename_path)`</strong></summary>

```python
# Code for the function process_image
def process_image(input_filename_path, output_filename_path):
    image = sitk.ReadImage(input_filename_path) # Load the nifti image
    output_image = sitk.Threshold(image, lower=0, upper=label_number, outsideValue=0) # Threshold the image: values above label_number (global variable definied in a flag) are set to 0, all other values remain unchanged
    sitk.WriteImage(output_image, output_filename_path)
```

</details>


##  



:point_right: **Create_split_json(train_list, val_list, current_script)** :point_left:
- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates and sets up necessary components for the `create_split_json`. There are 2 possibilities if function of the value of current_script (if train or transfer learning)
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
- `train_list` (list): All the images in used for the training
- `val_list` (list): All the images in used for the training
- ![Returns](https://img.shields.io/badge/-Returns-red) None
<details>
  <summary>Click to view the code for the function `Create_split_json( )`</summary>
  
```python
# Code for the function create_split_json
def create_split_json(train_list, val_list, current_script): #Note that here, as we use only fold 0 or fold all, we don't need to specify all the separation in all the other folds. You will need to complete this function in order to randomize the distribution train/validate for each fold
    if current_script == "train":
        data_list = [{"train": train_list, "val": val_list}] #Add all the image named train in the training and all of the validate image in the val

        os.makedirs(os.path.join(globalPath.nnunet_preprocessed_path, full_dataset_name))
        json_split_path = os.path.join(globalPath.nnunet_preprocessed_path, full_dataset_name, "splits_final.json") #Create the split json file
        with open(json_split_path, 'w') as json_file:
            json.dump(data_list, json_file, indent=4)

    elif current_script == "transferLearning":
        list_new_data() 
        new_json()  
        copy_json_file()
```
</details>


##  


:point_right: **List_new_data()** :point_left:
- ![Purpose](https://img.shields.io/badge/-Purpose-green) Add the new images into the list
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None
<details>
  <summary>Click to view the code for the function `List_new_data( )`</summary>
  
```python
# Code for the function create_split_json
def list_new_data():
    global new_data

    split_json_path = os.path.join(globalPath.model_folder_path, full_dataset_name, split_final_json) #Path to the split final json
    jsonfile = split_json_path

    with open(jsonfile,"r") as file:
        data = json.load(file)
        for f in os.listdir(os.path.join(globalPath.nnunet_raw_path, full_dataset_name,"imagesTr")):
            f = f.split("_")[0]
            if f not in data[0]["val"] and f not in data[0]["train"]:
                new_data.append(f) #Adding the value in the list if it is not present in the training or validation

    os.makedirs(os.path.join(globalPath.nnunet_preprocessed_path, dataset_source_name))

    for files in os.listdir(os.path.join(globalPath.model_folder_path, full_dataset_name)):
        if files == "nnUNetPlans.json":
            shutil.copy2(os.path.join(globalPath.model_folder_path, full_dataset_name, files), os.path.join(globalPath.nnunet_preprocessed_path, dataset_source_name, files))

```
</details>


##


:point_right: **New_json()** :point_left:
- ![Purpose](https://img.shields.io/badge/-Purpose-green) Add the new data into the right json file
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None
<details>
  <summary>Click to view the code for the function `List_new_data( )`</summary>
  
```python
# Code for the function create_split_json
def new_json():
    split_json_path = os.path.join(globalPath.model_folder_path, full_dataset_name, split_final_json)
    jsonfile = split_json_path

    with open(jsonfile,"r") as file:
        data = json.load(file)
            
        for j in range (len(new_data)):
            if name_img_dic[new_data[j]] == "validate":
                data[0]["val"].append(new_data[j])

            elif name_img_dic[new_data[j]] == "train":
                data[0]["train"].append(new_data[j])

    with open(jsonfile, "w") as file:
        json.dump(data, file, indent=4) 

```
</details>


##


:point_right: **Copy_json_file()** :point_left:
- ![Purpose](https://img.shields.io/badge/-Purpose-green) Copy the new json file that contain all the information
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None
<details>
  <summary>Click to view the code for the function `List_new_data( )`</summary>
  
```python
# Code for the function create_split_json
def copy_json_file():
    split_json_path = os.path.join(globalPath.model_folder_path, full_dataset_name, split_final_json)
    copy_folder_path = os.path.join(globalPath.nnunet_preprocessed_path, full_dataset_name)
    os.makedirs(copy_folder_path)
    shutil.copy2(split_json_path, os.path.join(copy_folder_path, split_final_json)) #Name of the json file is always splits_final.json in this case 

```
</details>


##


:point_right: **Get_channel_names( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Fetches channel names required for the nnUNet JSON structure.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
   - `image_type` (str):???????????? 
- ![Returns](https://img.shields.io/badge/-Returns-red)
   -`channels` (list): list of the channels name

<details>
  <summary><strong>Click to view the code for the function `Get_channel_names( )`</strong></summary>

```python
# Code for the function get_channel_names
def get_channel_names():
    channels = {}
    num_channels = 1
    for i in range(num_channels):
        channel_name = image_type
        channels[str(i)] = channel_name
    return channels
```

</details>


##  

:point_right: **Get_labels( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Retrieves labels for the nnUNet JSON structur
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
 - `label_number` (int): ????????????
- ![Returns](https://img.shields.io/badge/-Returns-red) 
  - `labels` (dict): A dictionary with label names and their corresponding indices

<details>
  <summary><strong>Click to view the code for the function `Get_labels( )`</strong></summary>

```python
# Code for the function get_labels
def get_labels():
    labels = {}
    num_labels = label_number + 1  
    for i in range(num_labels):
        if i == 0:
            label_name_fct = "background"
            labels[label_name_fct] = i
        else:
            labels[f"Label {i}"] = i
    return labels
```

</details>


##


:point_right: **Launch_docker(dataset_full_name, current_script)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) It is this function that will actually start the nnUNet model
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
 - `dataset_full_name` (str): Name of the dataset
 - `current_script` (str): If it is "train" or "transfer validation"
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Launch_docker( )`</strong></summary>

```python
# Code for the function get_labels
#Function for the terminal to do and starts the training 
def launch_docker(dataset_full_name, current_sript):
    global container_id
    dataset_id = dataset_full_name.split("_")[0].replace("Dataset", "")
    
    load_image() #Loading the docker image 
    
    # Execute the Docker command
    docker_command = f"docker run -d -it --gpus all --shm-size 8g -v {globalPath.dataset_train_path}:/app/nnUNet {image_docker} bash"
    container_id = subprocess.check_output(docker_command, shell=True).decode().strip()

    if current_sript == "train":
        #Execute other commands
        #gpu_number = gpu_available()[0] #Take the first available gpu on the list, Uncomment if you want to use this function 
        gpu_number = 1 #In this case, we use the GPU 0 for the training and the GPU for the inference
    
        global_commands = f"CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_plan_and_preprocess -d {dataset_id} -c {configuration_model} --verify_dataset_integrity"
        delete_all.exec_in_docker(global_commands, container_id) #Execute the command inside the docker container

        #Calcul the remaining time to see if there is still enough time to actually starts the training
        timer_training_end = tm.time()
        elapsed_time_training = (timer_training_end - timer_training_start) / 60 
        total_training_time = time_input - elapsed_time_training
        print(f"Time left for the training: {total_training_time}")

        if total_training_time <= 0: #In the case we don't have enough time, we stop the process
            print("Not enough time was given to train the model, try with a higher time")
            delete_all.clean_all(delete_input_folder=True, delete_output_folder=True, delete_model_folder=False, delete_all_nnunet_folder=True, script="train") #Clean all the folder to make sure we don't have any problems for the next training
            sys.exit()

        else: #If enough time, start the actual training of the nnUNet
            print("Starting training...")
            if not fold_all_value:
                global_commands = f"echo {int(total_training_time)} | CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_train {dataset_id} {configuration_model} 0 --npz" #See nnUNet document to have a better understanding but we need the GPU, dataset_id, configuration of the model and the value for the fold 
                delete_all.exec_in_docker(global_commands, container_id) 

            elif fold_all_value:
                global_commands = f"echo {int(total_training_time)} | CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_train {dataset_id} {configuration_model} all --npz"  
                delete_all.exec_in_docker(global_commands, container_id) 

            """ ---------------UNCOMMENT IF MANY FOLDS AND SEE THE BEST CONFIGURATION-------------------------
            global_commands = f"nnUNetv2_find_best_configuration {dataset_id} -c {configuration_model}"    
            exec_in_docker(global_commands) 
            """

        #Once the training is done we can close the docker container and move all the results inside the right folder
        remove_docker_container(container_id)
        move_result()
        delete_all.clean_all(delete_input_folder=True, delete_output_folder=False, delete_model_folder=False, delete_all_nnunet_folder=True, script="train") #Everything is deleted at the end to clean up

    elif current_script == "transferLearning":
        creation_checkpoint_folder()

        #gpu_number = gpu_available()[0] #Take the first available gpu on the list, Uncomment if you want to use this function 
        gpu_number = 1 #In this case, we use the GPU 0 for the training and the GPU for the inference

        global_commands = f"CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_plan_and_preprocess -d {dataset_id} -c 3d_fullres --verify_dataset_integrity"
        delete_all.exec_in_docker(global_commands, container_id)

        timer_training_end = tm.time()
        elapsed_time_training = (timer_training_end - timer_pretraining_start) / 60 
        total_training_time = time_input - elapsed_time_training
        print(f"Time left for the pretraining: {total_training_time}")

        if total_training_time <= 0: #Check if the user input time is enough to train the model after the preprocessing is done
            print("Not enough time was given to pretrain the model, try with a higher time")
            delete_all.clean_all(delete_input_folder=True, delete_output_folder=True, delete_model_folder=True, delete_all_nnunet_folder=True, script="transferLearning") #Clean all the folder to make sure we don't have any problems for the next training
            sys.exit()

        else:
            print("Moving plans between datasets...")
            global_commands = f"nnUNetv2_move_plans_between_datasets -s {999} -t {dataset_id} -sp nnUNetPlans -tp nnUNetPlans"
            delete_all.exec_in_docker(global_commands, container_id)

            print("Starting transfer learning...")
            if not fold_all_value:  
                docker_result_path = os.path.join("/app", "nnUNet", "nnUNet_results", dataset_source_name, "nnUNetTrainer__nnUNetPlans__3d_fullres", f"fold_{fold_0_or_all_value}", "checkpoint_final.pth")
                global_commands = f"echo {int(total_training_time)} | CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_train {dataset_id} 3d_fullres 0 -pretrained_weights {docker_result_path}"
                delete_all.exec_in_docker(global_commands, container_id) 

            else:  
                docker_result_path = os.path.join("/app", "nnUNet", "nnUNet_results", dataset_source_name, "nnUNetTrainer__nnUNetPlans__3d_fullres", f"fold_{fold_0_or_all_value}", "checkpoint_final.pth")
                global_commands = f"echo {int(total_training_time)} | CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_train {dataset_id} 3d_fullres all -pretrained_weights {docker_result_path}"
                delete_all.exec_in_docker(global_commands, container_id) 

            """UNCOMMENT IF ALL FOLDS ARE USED
            print("Finding best configurations...")
            global_commands = f"nnUNetv2_find_best_configuration {dataset_id} -c 3d_fullres"    
            exec_in_docker(global_commands) 
            """

        #Once the training is done we can close the docker container and move all the results inside the right folder
        remove_docker_container(container_id)
        move_result()
        delete_all.clean_all(delete_input_folder=True, delete_output_folder=False, delete_model_folder=True, delete_all_nnunet_folder=True, script="transferLearning") #Everything is deleted at the end to clean up

```

</details>


##


:point_right: **Load_image( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Load nnUNet docker images
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Load_image( )`</strong></summary>

```python
# Code for the function load_image
def load_image():
    exec_command = f"docker load -i {grandparent_main_path}/{image_docker}.tar"
    subprocess.call(exec_command, shell=True)
```
</details>


##


:point_right: **Gpu_available( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Decodes the result and splits it into lines to determine GPU availability
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red)
   - `available_gpus` (list): list of all the available GPUs

<details>
  <summary><strong>Click to view the code for the function `Gpu_available( )`</strong></summary>

```python
# Code for the function gpu_available
def gpu_available():
    result = subprocess.run(['nvidia-smi', '--query-gpu=index,utilization.gpu', '--format=csv,noheader,nounits'], stdout=subprocess.PIPE)
    # Decode the output and split it into lines
    lines = result.stdout.decode('utf-8').strip().split("\n")
    available_gpus = [] # List to store indices of available GPUs

    for line in lines:
        index, util = line.split(", ")
        if int(util) < 10:
            available_gpus.append(index)

    # Check the number of available GPUs and act accordingly
    if not available_gpus:
        print("No GPUs are available, try later.")
        delete_all.launch_docker(delete_input_folder=True)
        sys.exit()

    return available_gpus
```
</details>


##


:point_right: **creation_checkpoint_folder( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates the different folder for the transfer learning
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Load_image( )`</strong></summary>

```python
# Code for the function load_image
def creation_checkpoint_folder():
    os.makedirs(os.path.join(globalPath.nnunet_result_path, dataset_source_name))
    for folder in os.listdir(globalPath.model_folder_path):
        for files in os.listdir(os.path.join(globalPath.model_folder_path, folder)):
            if os.path.isdir(os.path.join(globalPath.model_folder_path, folder, files)):
                shutil.copytree(os.path.join(globalPath.model_folder_path, folder, files) , os.path.join(globalPath.nnunet_result_path, dataset_source_name, files)) #Copy the models inside the Dataset train like that it can acces the weight
            elif os.path.isfile(os.path.join(globalPath.model_folder_path, folder, files)):
                shutil.copy2(os.path.join(globalPath.model_folder_path, folder, files) , os.path.join(globalPath.nnunet_result_path, dataset_source_name, files))

```
</details>


##


:point_right: **Remove_docker_container(id)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Remove a Docker container based on a specified name or ID
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
 - `id` (int ???): ID of the container
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Remove_docker_container(id)`</strong></summary>

```python
# Code for the function remove_docker_container
def remove_docker_container(id):
    global_commands = f"docker stop {id}"
    subprocess.check_output(global_commands, shell=True, stderr=subprocess.STDOUT)

    global_commands = f"docker rm {id}"
    subprocess.check_output(global_commands, shell=True, stderr=subprocess.STDOUT)

    print(f"Docker container id: {id} has been removed")
```

</details>


##  


:point_right: **Move_result( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Handles the process of moving results in the right emplacement 
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Move_result( )`</strong></summary>

```python
# Code for the function move_result
def move_result():
    for folder in os.listdir(globalPath.nnunet_result_path): #For loop inside the result folder of the nnUNet (usually, it is only 1 folder)
        if folder != "Dataset999_SOURCE":
            tot_path = os.path.join(globalPath.output_folder_path, folder)
            shutil.copytree(os.path.join(globalPath.nnunet_result_path, folder), tot_path) #Copy everything to the Output folder
            new_tot_path = os.path.join(tot_path, "nnUNetTrainer__nnUNetPlans__3d_fullres") #Change here also if you are using another configuration for the model

            for new_folder in os.listdir(new_tot_path): #For loop inside the output folder, to keep only the needed file
                path_final = os.path.join(new_tot_path, new_folder)
                if os.path.isdir(path_final) and new_folder.split("_")[0] == "fold":
                    tot_path_fold = ""
                    if not fold_all_value: #Be careful, if you modify the code to use different fold, you will need to change this!
                        tot_path_fold = os.path.join(new_tot_path, "fold_0")
                    else:
                        tot_path_fold = os.path.join(new_tot_path, "fold_all")

                    for files in os.listdir(tot_path_fold): #Continung looping inside the results folder (structure of the nnUNet)
                        if files != "checkpoint_final.pth" and files.split("_")[0] != "training" and files != "progress.png": #We keep only the final weights of the model, the training log and the progress image, all of the other files/folder will be deleted
                            path_to_check = os.path.join(tot_path_fold, files)
                            if os.path.isfile(path_to_check):
                                os.remove(path_to_check)
                            elif os.path.isdir(path_to_check):
                                shutil.rmtree(path_to_check)

                elif os.path.isdir(path_final): #We don't need to keep all of the folder that doesn't start with "fold"
                    path_to_del = os.path.join(new_tot_path, new_folder)
                    shutil.rmtree(path_to_del)

            #We need also different files that are located in the preprocessed nnUNet folder (to do the Transfer Learning later)
            for files in os.listdir(os.path.join(globalPath.nnunet_preprocessed_path, folder)): #For loop in the nnUNet preprocessed folder
                if files == "splits_final.json": #We need to keep the splits_final json file
                    shutil.copy2(os.path.join(globalPath.nnunet_preprocessed_path, folder, files), os.path.join(globalPath.output_folder_path, folder, files))
                    print("Copy splits_final.json file!")

                elif files == "nnUNetPlans.json": #We need to keep the nnUnetPlans json file
                    shutil.copy2(os.path.join(globalPath.nnunet_preprocessed_path, folder, files), os.path.join(globalPath.output_folder_path, folder, files))
                    print("Copy nnUNetPlans.json file!")

            #We need also one fils that is located in the raw nnUNet folder (to do the Transfer Learning later)    
            for files in os.listdir(globalPath.dataset_train_path):
                if files == "info_model.json": #We need to keep the info model json that we created to get some additionnal information about the model
                    shutil.copy2(os.path.join(globalPath.dataset_train_path, files), os.path.join(globalPath.output_folder_path, folder, files))
                    os.remove(os.path.join(globalPath.dataset_train_path, files))
                    print("Copy info_model.json file!")

    print("Model saved and cleaned!")
```

</details>

##







