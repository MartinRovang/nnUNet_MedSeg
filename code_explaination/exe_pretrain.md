
## Documentation for `exe_train.py`

---

### Overview

The `exe_pretrain.py` script is designed for finetune an existing model to make it more accurate.

### Table of Contents

- [Prerequisites](#prerequisites)
- [Main Execution](#main-execution)
- [Functions](#functions)
- [Usage](#usage)

---

### Prerequisites

Ensure you have the following libraries installed:

- os
- json
- shutil
- sys
- subprocess
- argparse
- SimpleITK
- time
- datetime
- random

---

:point_right: Main Execution :point_left:







---

### Functions

:point_right:check_for_train_or_validate:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Checks if there's a file named 'train' or 'validate' in the directory.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `directory`(str): Path to the directory to check.
- ![Returns](https://img.shields.io/badge/-Returns-red)
   - `True` if training or validation images are found.
  - `False` otherwise.

<details>
  <summary>Click to view the code for the function `check_for_train_or_validate`</summary>

```python
# Code for the function check_for_train_or_validate
```

</details>

##  

:point_right:process_image:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Processes a NIfTI image to retain only a specified label.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `input_filename_path` (str): Path to the input image.
  - `output_filename_path` (str): Path to save the processed image.
- ![Returns](https://img.shields.io/badge/-Returns-red) The processed image is saved to the specified path.

<details>
  <summary>Click to view the code for the function `process_image`</summary>

```python
# Code for the function process_image
```

</details>

##  

:point_right:get_model_name:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Get model name which has to be finetuned.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `model_folder_path` (str): path to the `model` folder.
- ![Returns](https://img.shields.io/badge/-Returns-red) Update full_dataset_name.

<details>
  <summary>Click to view the code for the function `get_model_name`</summary>

```python
# Code for the function get_model_name
```

</details>

##  

:point_right:get_fold_value:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Check the fold value.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - Path to the `fold` folder 
- ![Returns](https://img.shields.io/badge/-Returns-red) return the folder value

<details>
  <summary>Click to view the code for the function `get_fold_value`</summary>

```python
# Code for the function get_fold_value
```

</details>

##  

:point_right:remove_folder_model:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Delete the content of `model` folder 
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  -  `model_folder_path` (str): path to the `model` folder.
- ![Returns](https://img.shields.io/badge/-Returns-red) None.

<details>
  <summary>Click to view the code for the function `remove_folder_model`</summary>

```python
# Code for the function remove_folder_model
```

</details>

##  

:point_right:list_new_data:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Sort the data into 'val' and 'train', keep previous data in the original split
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `data_tot_path`: Path or directory
- ![Returns](https://img.shields.io/badge/-Returns-red) ?????????????????

<details>
  <summary>Click to view the code for the function `list_new_data`</summary>

```python
# Code for the function list_new_data
```

</details>

##  

:point_right:new_json:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Write a new JSON file with the right split
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red) new JSON file.

<details>
  <summary>Click to view the code for the function `new_json`</summary>

```python
# Code for the function new_json
```

</details>

##  

:point_right:copy_json_file:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Copy the JSON file in the right folder
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red) Copied the JSON file onto splits_final.json

<details>
  <summary>Click to view the code for the function `copy_json_file`</summary>

```python
# Code for the function copy_json_file
```

</details>

##  

:point_right:create_split_json:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates and sets up necessary components for the create_split_json.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
- ![Returns](https://img.shields.io/badge/-Returns-red) Doesn't return a value.

<details>
  <summary>Click to view the code for the function `create_split_json`</summary>

```python
# Code for the function create_split_json
```

</details>

##  

:point_right:get_channel_names:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Fetches channel names required for the nnUNet JSON structure.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): 
  - A dictionary with channel names.

<details>
  <summary>Click to view the code for the function `get_channel_names`</summary>

```python
# Code for the function get_channel_names
```

</details>

##  

:point_right:get_labels:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Retrieves labels for the nnUNet JSON structure.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): 
  - A dictionary with label names and their corresponding indices.

<details>
  <summary>Click to view the code for the function `get_labels`</summary>

```python
# Code for the function get_labels
```

</details>

##  

:point_right:create_structure:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Creating the main folder directory (with the right name).
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red):

- `Dataset_pretrain`
  - `nUNet raw`
  - `nnUNet_preprocessed`
  - `nnUNet results`
      


<details>
  <summary>Click to view the code for the function `create_structure`</summary>

```python
# Code for the function create_structure
```

</details>

##  

:point_right:move_result():point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Copy all the results needed for the user in the output file
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
   -`checkpoint_final.pth`
  - `splits_final.json`
  - `nnUNetPlans.json`
  - `info_model.json`
- ![Returns](https://img.shields.io/badge/-Returns-red)
  - `output_pretrain`

<details>
  <summary>Click to view the code for the function `move_result`</summary>

```python
# Code for the function move_result
```

</details>

##  

:point_right:delete_all_folders(path_folder, docker_path):point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Delete all the useless folders
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `path_folder`; path to the folder we want to delete
  - `docker_path`: path to the docker nnUNet
- ![Returns](https://img.shields.io/badge/-Returns-red) Free space folders

<details>
  <summary>Click to view the code for the function `delete_all_folders`</summary>

```python
# Code for the function delete_all_folders
```

</details>

##  

:point_right:remove_docker_container(id):point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Stop and remove the Docker container
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `id`: id of the container
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `remove_docker_container`</summary>

```python
# Code for the function remove_docker_container
```

</details>

##  

:point_right:clean_all():point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Open the container, call the previous function to delete the folders and close the container 
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `clean_all`</summary>

```python
# Code for the function clean_all
```

</details>

##  

:point_right:gpu_available():point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Check if GPU available (Use nbr.1)
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - Use nvidia-smi
- ![Returns](https://img.shields.io/badge/-Returns-red) Return a list of the GPU's available

<details>
  <summary>Click to view the code for the function `gpu_available`</summary>

```python
# Code for the function gpu_available
```

</details>

##  

:point_right:exec_in_docker(cmd):point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Function that is called when we have to execute a command in the docker
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `cmd`: Command that we wanted to execute
- ![Returns](https://img.shields.io/badge/-Returns-red) Results of this execution

<details>
  <summary>Click to view the code for the function `exec_in_docker`</summary>

```python
# Code for the function exec_in_docker
```

</details>

##  

:point_right:creation_checkpoint_folder():point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red) Doesn't return a value.

<details>
  <summary>Click to view the code for the function `creation_checkpoint_folder`</summary>

```python
# Code for the function creation_checkpoint_folder
```

</details>

##  
 
:point_right:load_image:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red) Doesn't return a value.

<details>
  <summary>Click to view the code for the function `load_image`</summary>

```python
# Code for the function load_image
```

</details>

##  

:point_right:launch_docker:point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red) Doesn't return a value.

<details>
  <summary>Click to view the code for the function `launch_docker`</summary>

```python
# Code for the function launch_docker
```

</details>

---

:point_right:Usage:point_left:

To execute the `exe_pretrain.py` script, use the following command:

```
python exe_pretrain.py [-l LABEL] [-i IMAGE_TYPE] [-t TIME]
```

Arguments:
- `-l` or `--label`: Label to be used (default: "TUMOR").
- `-i` or `--image_type`: Type of image (default: "CT").
- `-t` or `--time`: Time parameter (default: 60).


