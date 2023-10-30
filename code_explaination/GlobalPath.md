
## Documentation for `GlobalPath.py`

---

### Overview

The `GlobalPath.py` serves as a central hub for consolidating various paths required by different scripts. This approach aims to tidy up the scripts, resulting in cleaner and more comprehensible code.

---



### Code

Only 1 function is in the code. The global variables (which are all the different paths) are defined wether it is in training or transfer learning.



:point_right: **MyPath(script)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Define the correct path
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `script` (str): In what case the path is needed
- ![Returns](https://img.shields.io/badge/-Returns-red) None


<details>
  <summary><strong>Click to view the code for the function `MyPath( )`</strong></summary>

```python
# Code for the function create_split_json
import os
import sys

#MAIN PATHS
main_path = os.path.dirname(os.path.abspath(__file__))  # Get the parent path of the main folder

nnunet_preprocessed_path = None
docker_nnunet_preprocessed_path = None
nnunet_result_path = None
docker_nnunet_result_path = None
nnunet_raw_path = None
docker_nnunet_raw_path = None
docker_nnunet_output_path = None
docker_nnunet_input_path = None
input_folder_path = None
output_folder_path = None
dataset_train_path = None
model_folder_path = None
docker_model_path = None

def myPath(script):
    global nnunet_preprocessed_path, docker_nnunet_preprocessed_path, nnunet_result_path, docker_nnunet_result_path
    global nnunet_raw_path, docker_nnunet_raw_path, docker_nnunet_output_path
    global docker_nnunet_input_path
    global input_folder_path, output_folder_path, dataset_train_path
    global model_folder_path, docker_model_path

    if script == "train":
        input_folder_name = "Input_nnUNet_train"
        output_folder_name = "Output_model"

        input_folder_path = os.path.join(main_path, "train", input_folder_name)
        output_folder_path = os.path.join(main_path, "train", output_folder_name)
        dataset_train_path = os.path.join(main_path, "train", "Dataset_Train")  # Here is the full path name of the directory file

        nnunet_raw_path = os.path.join(dataset_train_path, "nnUNet_raw")
        nnunet_preprocessed_path = os.path.join(dataset_train_path, "nnUNet_preprocessed")
        nnunet_result_path = os.path.join(dataset_train_path, "nnUNet_results")

        # DOCKER PATH
        docker_nnunet_raw_path = "/app/nnUNet/train/Dataset_Train/nnUNet_raw"
        docker_nnunet_preprocessed_path = "/app/nnUNet/train/Dataset_Train/nnUNet_preprocessed"
        docker_nnunet_result_path = "/app/nnUNet/train/Dataset_Train/nnUNet_results"
        docker_nnunet_input_path = "/app/nnUNet/train/Input_nnUNet_train"
        docker_nnunet_output_path = "/app/nnUNet/train/Output_model"

    elif script == "transferLearning":
        input_folder_name = "Input_transferLearning"
        output_folder_name = "Output_transferLearning"

        input_folder_path = os.path.join(main_path, "transferLearning", input_folder_name)
        output_folder_path = os.path.join(main_path, "transferLearning", output_folder_name)
        dataset_train_path = os.path.join(main_path, "transferLearning", "Dataset_transferLearning") #Here is the full path name of the directory file
        model_folder_path = os.path.join(main_path, "transferLearning", "model")

        nnunet_raw_path = os.path.join(dataset_train_path, "nnUNet_raw")
        nnunet_preprocessed_path =  os.path.join(dataset_train_path, "nnUNet_preprocessed")
        nnunet_result_path =  os.path.join(dataset_train_path, "nnUNet_results")

        #DOCKER path
        docker_nnunet_raw_path = "/app/nnUNet/transferLearning/Dataset_transferLearning/nnUNet_raw"
        docker_nnunet_preprocessed_path = "/app/nnUNet/transferLearning/Dataset_transferLearning/nnUNet_preprocessed"
        docker_nnunet_result_path = "/app/nnUNet/transferLearning/Dataset_transferLearning/nnUNet_results"
        docker_nnunet_input_path = "/app/nnUNet/transferLearning/Input_transferLearning"
        docker_nnunet_output_path = "/app/nnUNet/transferLearning/Output_transferLearning"
        docker_model_path = "/app/nnUNet/transferLearning/model"

    else:
        print("Error in the keywords to define all the paths")
        sys.exit()

```





---



