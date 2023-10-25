## Documentation for `generalFunctions.py`

---

### Overview

The `generalFunctions.py` script is designed to clean up the code and contains all the functions that are general for both scripts

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
- datetime
- exe_train
- exe_transferLearning
- delete_all


---

### Functions


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

:point_right: **Create_structure( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates the main folder directory (with the right name) + all the necessary json files
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
 - `train` (???): ????????????
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Create_structure( )`</strong></summary>

```python
def create_structure():
    global full_dataset_name, fold_all_value

    #Creating the main folder directory (with the right name)
    next_number = 1 
    main_folder_name = f"Dataset{next_number:03}_{dataset_name}"  #Formatting the number to be 3 digits
    full_dataset_name = main_folder_name
    main_folder_path = os.path.join(nnunet_raw_path , main_folder_name)  # Combine with actual_path (nnunet raw folder)
    if not os.path.exists(main_folder_path): #Check if the name already exists (normally not because everything is deleted after each training)
        os.makedirs(main_folder_path)
    else:
        print(f"Folder {main_folder_name} already exists.")
        return

    #Create 2 sub-folders inside the main folder
    subfolders = ['imagesTr', 'labelsTr']
    for subfolder in subfolders:
        os.makedirs(os.path.join(main_folder_path, subfolder))

    #Definition of paths and variables
    img_destination = os.path.join(nnunet_raw_path, main_folder_name, "imagesTr") 
    train_destination = os.path.join(nnunet_raw_path, main_folder_name, "labelsTr")
    num_training = 0
    num_images = 0
    tr_cases = 0
    val_cases = 0
    train_img_list = []
    validate_img_list=[]

    #Moving the images in the right directory
    for directory in os.listdir(input_folder_path): #For loop on the input folder (there should be only 1 folder inside!)
        directory_path = os.path.join(input_folder_path, directory)

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
        create_split_json(train_img_list, validate_img_list) #Split json is created to use the right image in the training and in the validation 

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
        json_file_path = os.path.join(dataset_train_path, 'info_model.json')
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
        for directory in os.listdir(input_folder_path): 
            directory_path = os.path.join(input_folder_path, directory)
            shutil.rmtree(directory_path)
            print(f"Input folder ({directory}) has been deleted")

        launch_docker(main_folder_name) #Once the images are well separated, the training can start

    else: #If there is a mismatch in the number of images, clean all the folders + stops the code
        print("ERROR number of images")
        delete_all.launch_docker(delete_input_folder=True)
        sys.exit()
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
    for folder in os.listdir(nnunet_result_path): #For loop inside the result folder of the nnUNet (usually, it is only 1 folder)
        tot_path = os.path.join(output_folder_path, folder)
        shutil.copytree(os.path.join(nnunet_result_path, folder), tot_path) #Copy everything to the Output folder
        new_tot_path = os.path.join(tot_path, f"nnUNetTrainer__nnUNetPlans__{configuration_model}")

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
        for files in os.listdir(os.path.join(nnunet_preprocessed_path, folder)): #For loop in the nnUNet preprocessed folder
            if files == "splits_final.json": #We need to keep the splits_final json file
                shutil.copy2(os.path.join(nnunet_preprocessed_path, folder, files), os.path.join(output_folder_path, folder, files))
                print("Copy splits_final.json file!")

            elif files == "nnUNetPlans.json": #We need to keep the nnUnetPlans json file
                shutil.copy2(os.path.join(nnunet_preprocessed_path, folder, files), os.path.join(output_folder_path, folder, files))
                print("Copy nnUNetPlans.json file!")

        #We need also one fils that is located in the raw nnUNet folder (to do the Transfer Learning later)    
        for files in os.listdir(dataset_train_path):
            if files == "info_model.json": #We need to keep the info model json that we created to get some additionnal information about the model
                shutil.copy2(os.path.join(dataset_train_path, files), os.path.join(output_folder_path, folder, files))
                os.remove(os.path.join(dataset_train_path, files))
                print("Copy info_model.json file!")

    print("Model saved and cleaned!")
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

:point_right: **Exec_in_docker(cmd, container_id)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Executes commands within the Docker container
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
   - `cmd` (str): Command to execute inside the docker container
   - `container_id` (int ???): ID of the container
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Exec_in_docker(cmd, container_id)`</strong></summary>

```python
# Code for the function exec_in_docker
def exec_in_docker(cmd):
    exec_command = f"docker exec -i {container_id} bash -c '{cmd}'"
    result = subprocess.call(exec_command, shell=True)
    return result
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

