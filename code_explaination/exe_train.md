
## Documentation for `exe_train.py`

----------

### Overview

The `exe_train.py` script is designed for processing and preparing NIfTI (.nii) images for the nnUNet framework, a renowned deep learning framework for biomedical image segmentation.

### Table of Contents

- [Prerequisites](#prerequisites)
- [Functions](#functions)
- [Main Execution](#main-execution)
- [Usage](#usage)

----------

### Prerequisites

Ensure you have the following libraries installed:

- os
- json
- shutil
- sys
- subprocess
- argparse
- SimpleITK
- delete_all (other python script in the same project)

----------

### Functions

:point_right: Main Execution :point_left:

1. Definition of all the different needed path for the process and the global variables
2. Checks if the input folder exists
3. If found, 3 different cases might happen:
  - 0 folder inside the input folder. This means that the data is not placed correctly, the code stops.
  - More than 1 folder is found. This means that there are too many folder. launch_docker function from delete_all.py is called to clean up and then stops the code.
  - Only 1 folder is found. The code continues correctly, all the global variables are definied in respect with the values of the flags of the command line. Finally, the function "create_structure" is called to start the process.
4. If not found, it exits, indicating the missing folder

<details>
  <summary><strong> Click to view the code for the main execution</strong></summary>

```python
#MAIN PATHS 
main_path = os.path.dirname(os.path.abspath(__file__)) #Get the parent path of the main folder
grandparent_main_path = os.path.dirname(main_path)
input_folder_name = "Input_nnUNet_train"
output_folder_name = "Output_model"
input_folder_path = os.path.join(main_path, input_folder_name)
output_folder_path = os.path.join(main_path, output_folder_name)
dataset_train_path = os.path.join(main_path, "Dataset_Train") #Here is the full path name of the directory file
nnunet_raw_path = os.path.join(dataset_train_path, "nnUNet_raw")
nnunet_preprocessed_path =  os.path.join(dataset_train_path, "nnUNet_preprocessed")
nnunet_result_path =  os.path.join(dataset_train_path, "nnUNet_results")
delete_all_script_path = os.path.join(grandparent_main_path, "delete_all.py")


#VARIABLES
full_dataset_name = ""
dataset_name = ""
label_number = 0
image_type = ""
time_input = 0
image_docker = "nnunet_timev22"
file_ending = ".nii.gz"
configuration_model = ""
fold_all_value = False



if input_folder_path:
    if len(os.listdir(input_folder_path)) == 0: #This means that the data was not added into the right folder
        print("Input folder is empty!")
        sys.exit() 

    elif len(os.listdir(input_folder_path)) > 1: #This case is not possible, just clean everything and stop the process
        delete_all.launch_docker(delete_input_folder=True)
        print("Too many input folders, everything was cleaned, launch the training again!")
        sys.exit()

    else:
        print(f"Found {input_folder_name} at: {input_folder_path}")
        delete_all.launch_docker(delete_input_folder=False) #To clean everything up in case something went wrong before
        if __name__ == "__main__":
            #Get the values of the input command
            timer_training_start = tm.time()
            parser = argparse.ArgumentParser()
            parser.add_argument("-d", "--dataset_name", dest="dataset_name", type=str, default="No_Name")
            parser.add_argument("-l", "--label", dest="label", type=int)
            parser.add_argument("-i", "--image_type", dest="image_type", type=str, default= "CT")
            parser.add_argument("-t", "--time", dest="time", type=int, default=60)
            parser.add_argument("-c", "--configuration_model", dest="configuration_model", type=str, default= "3d_fullres")
            args = parser.parse_args()
            dataset_name = args.dataset_name
            label_number = args.label
            image_type = args.image_type
            time_input = args.time
            configuration_model = args.configuration_model

            #Main code to run
            create_structure()
            
else:
    print(f"{input_folder_name} not found.")
    sys.exit()
```
</details>



##  




:point_right: Create_structure( ) :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates the main folder directory (with the right name) + all the necessary json files
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `create_structure`</strong></summary>

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


:point_right: Check_for_train_or_validate(directory) :point_left:

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


:point_right: Process_image(input_filename_path, output_filename_path) :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Processes a NIfTI image to retain only a specified label.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `input_filename_path` (str): Path to the input image.
  - `output_filename_path` (str): Path to save the processed image.
- ![Returns](https://img.shields.io/badge/-Returns-red): None. The processed image is saved to the specified path.

<details>
  <summary><strong>Click to view the code for the function `process_image`</strong><</summary>

```python
# Code for the function process_image
def process_image(input_filename_path, output_filename_path):
    image = sitk.ReadImage(input_filename_path) # Load the nifti image
    output_image = sitk.Threshold(image, lower=0, upper=label_number, outsideValue=0) # Threshold the image: values above label_number (global variable definied in a flag) are set to 0, all other values remain unchanged
    sitk.WriteImage(output_image, output_filename_path)
```

</details>


:point_right: Create_split_json(train_list, val_list) :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Constructs a JSON structure denoting training and validation splits.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `train_list` (list): List of training images.
  - `val_list` (list): List of validation images.
- ![Returns](https://img.shields.io/badge/-Returns-red): None. The JSON structure is saved in the appropriate directory.


<details>
  <summary><strong>Click to view the code for the function `create_split_json`</strong><</summary>

```python
# Code for the function create_split_json
def create_split_json(train_list, val_list): #Note that here, as we use only fold 0 or fold all, we don't need to specify all the separation in all the other folds. You will need to complete this function in order to randomize the distribution train/validate for each fold
    data_list = [{"train": train_list, "val": val_list}] #Add all the image named train in the training and all of the validate image in the val

    os.makedirs(os.path.join(nnunet_preprocessed_path, full_dataset_name))
    json_split_path = os.path.join(nnunet_preprocessed_path, full_dataset_name, "splits_final.json") #Create the split json file
    with open(json_split_path, 'w') as json_file:
        json.dump(data_list, json_file, indent=4)
```
</details>


:point_right: Get_channel_names( ) :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Fetches channel names required for the nnUNet JSON structure.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): 
  - A dictionary with channel names.

<details>
  <summary>Click to view the code for the function `get_channel_names`</summary>

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



#### get_labels

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Retrieves labels for the nnUNet JSON structure.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): 
  - A dictionary with label names and their corresponding indices.

<details>
  <summary>Click to view the code for the function `get_labels`</summary>

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




#### delete_all_folders

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Based on the function name, it is likely used to delete all folders in a specified path or perform some cleanup.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): None.

<details>
  <summary>Click to view the code for the function `delete_all_folders`</summary>

```python
# Code for the function delete_all_folders
```

</details>

#### remove_docker_container

- ![Purpose](https://img.shields.io/badge/-Purpose-green): This function is intended to remove a Docker container based on a specified name or ID.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): None.

<details>
  <summary>Click to view the code for the function `remove_docker_container`</summary>

```python
# Code for the function remove_docker_container
```

</details>



#### move_result

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Handles the process of moving results.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): None.

<details>
  <summary>Click to view the code for the function `move_result`</summary>

```python
# Code for the function move_result
```

</details>



#### gpu_available

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Decodes the output and splits it into lines to determine GPU availability.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): Boolean indicating if GPU is available.

<details>
  <summary>Click to view the code for the function `gpu_available`</summary>

```python
# Code for the function gpu_available
```

</details>

#### exec_in_docker

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Executes commands within the Docker container.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): None.

<details>
  <summary>Click to view the code for the function `exec_in_docker`</summary>

```python
# Code for the function exec_in_docker
```

</details>

#### load_image

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Function for the terminal to do image loading.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): None.

<details>
  <summary>Click to view the code for the function `load_image`</summary>

```python
# Code for the function load_image
```

</details>

#### launch_docker

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Handles the process of launching the Docker image.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): None.

<details>
  <summary>Click to view the code for the function `launch_docker`</summary>

```python
# Code for the function launch_docker
```

</details>

---



---

### Usage

To run the script, use:

```bash
python exe_train.py -d [DATASET_NAME] -l [LABEL] -i [IMAGE_TYPE] -t [TIME] -c [CONFIGURATION]
```

- `-d, --dataset_name`: Name of the dataset (default: "No_Name").
- `-l, --label`: Label number to retain in the image.
- `-i, --image_type`: Type of the image (default: "CT").
- `-t, --time`: Time parameter (default: 60).
- `-c, --configuration`: Configuration (default: 3d_fullres).

---

**Note**: This documentation serves as a starting point. Depending on additional functionalities or changes in the code, the documentation might require updates.

---

