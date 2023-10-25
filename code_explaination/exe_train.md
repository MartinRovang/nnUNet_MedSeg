
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

### Main Execution 

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

---



### Functions



:point_right: **Create_split_json(train_list, val_list)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Constructs a JSON structure denoting training and validation splits
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `train_list` (list): List of training images
  - `val_list` (list): List of validation images
- ![Returns](https://img.shields.io/badge/-Returns-red) None


<details>
  <summary><strong>Click to view the code for the function `Create_split_json( )`</strong></summary>

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


##  


:point_right: **Launch_docker( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Handles the process of launching the Docker image
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary><strong>Click to view the code for the function `Launch_docker( )`</strong></summary>

```python
# Code for the function launch_docker
#Function for the terminal to do 
def launch_docker(dataset_full_name):
    global container_id
    dataset_id = dataset_full_name.split("_")[0].replace("Dataset", "")
    
    load_image() #Loading the docker image 
    
    # Execute the Docker command
    docker_command = f"docker run -d -it --gpus all --shm-size 8g -v {dataset_train_path}:/app/nnUNet {image_docker} bash"
    container_id = subprocess.check_output(docker_command, shell=True).decode().strip()

    # Execute other commands
    #gpu_number = gpu_available()[0] #Take the first available gpu on the list, Uncomment if you want to use this function 
    gpu_number = 0 #In this case, we use the GPU 0 for the training and the GPU for the inference
    
    global_commands = f"CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_plan_and_preprocess -d {dataset_id} -c {configuration_model} --verify_dataset_integrity"
    exec_in_docker(global_commands) #Execute the command inside the docker container

    #Calcul the remaining time to see if there is still enough time to actually starts the training
    timer_training_end = tm.time()
    elapsed_time_training = (timer_training_end - timer_training_start) / 60 
    total_training_time = time_input - elapsed_time_training
    print(f"Time left for the training: {total_training_time}")

    if total_training_time <= 0: #In the case we don't have enough time, we stop the process
        print("Not enough time was given to train the model, try with a higher time")
        delete_all.launch_docker(delete_input_folder=True) #Clean all the folder to make sure we don't have any problems for the next training
        sys.exit()

    else: #If enough time, start the actual training of the nnUNet
        print("Starting training...")
        if not fold_all_value:
            global_commands = f"echo {int(total_training_time)} | CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_train {dataset_id} {configuration_model} 0 --npz" #See nnUNet document to have a better understanding but we need the GPU, dataset_id, configuration of the model and the value for the fold 
            exec_in_docker(global_commands) 

        elif fold_all_value:
            global_commands = f"echo {int(total_training_time)} | CUDA_VISIBLE_DEVICES={gpu_number} nnUNetv2_train {dataset_id} {configuration_model} all --npz"  
            exec_in_docker(global_commands) 

        """ ---------------UNCOMMENT IF MANY FOLDS AND SEE THE BEST CONFIGURATION-------------------------
        global_commands = f"nnUNetv2_find_best_configuration {dataset_id} -c {configuration_model}"    
        exec_in_docker(global_commands) 
        """

    #Once the training is done we can close the docker container and move all the results inside the right folder
    remove_docker_container(container_id)
    move_result()
    delete_all.launch_docker(delete_input_folder=True) #Everything is deleted at the end to clean up
```

</details>


---

### Usage

To run the script, use:

```bash
python exe_train.py -d [DATASET_NAME] -l [LABEL] -i [IMAGE_TYPE] -t [TIME] -c [CONFIGURATION_MODEL]
```

- `-d, --dataset_name`: Name of the dataset (default: "No_Name").
- `-l, --label`: Label number to retain in the image.
- `-i, --image_type`: Type of the image (default: "CT").
- `-t, --time`: Time parameter (default: 60).
- `-c, --configuration_model`: Configuration (default: 3d_fullres).

---


