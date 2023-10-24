
## Documentation for `exe_train.py`

---

### Overview

The `exe_train.py` script is designed for processing and preparing NIfTI (.nii) images for the nnUNet framework, a renowned deep learning framework for biomedical image segmentation.

### Table of Contents

- [Prerequisites](#prerequisites)
- [Functions](#functions)
- [Main Execution](#main-execution)
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

---

### Functions

#### check_for_train_or_validate

- <span style="color:green">**Purpose**</span>: Determines if the provided directory contains images designated for training or validation.
- <span style="color:blue">**Parameters**</span>: 
  - `directory` (str): Path to the directory to check.
- <span style="color:red">**Returns**</span>: 
  - `True` if training or validation images are found.
  - `False` otherwise.

<details>
  <summary>Click to view the code for the function `check_for_train_or_validate`</summary>

```python
# Code for the function check_for_train_or_validate
```

</details>

#### process_image

- <span style="color:green">**Purpose**</span>: Processes a NIfTI image to retain only a specified label.
- <span style="color:blue">**Parameters**</span>: 
  - `input_filename_path` (str): Path to the input image.
  - `output_filename_path` (str): Path to save the processed image.
- <span style="color:red">**Returns**</span>: None. The processed image is saved to the specified path.

<details>
  <summary>Click to view the code for the function `process_image`</summary>

```python
# Code for the function process_image
```

</details>

#### get_channel_names

- <span style="color:green">**Purpose**</span>: Fetches channel names required for the nnUNet JSON structure.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: 
  - A dictionary with channel names.

<details>
  <summary>Click to view the code for the function `get_channel_names`</summary>

```python
# Code for the function get_channel_names
```

</details>

#### get_labels

- <span style="color:green">**Purpose**</span>: Retrieves labels for the nnUNet JSON structure.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: 
  - A dictionary with label names and their corresponding indices.

<details>
  <summary>Click to view the code for the function `get_labels`</summary>

```python
# Code for the function get_labels
```

</details>

#### create_split_json

- <span style="color:green">**Purpose**</span>: Constructs a JSON structure denoting training and validation splits.
- <span style="color:blue">**Parameters**</span>: 
  - `train_list` (list): List of training images.
  - `val_list` (list): List of validation images.
- <span style="color:red">**Returns**</span>: None. The JSON structure is saved in the appropriate directory.


<details>
  <summary>Click to view the code for the function `create_split_json`</summary>

```python
# Code for the function create_split_json
```

</details>

#### get_labels

- <span style="color:green">**Purpose**</span>: This function appears to be designed to retrieve labels for the nnUNet JSON structure. Based on the provided label number, it generates a dictionary of labels.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: A dictionary with label names and their corresponding indices.

<details>
  <summary>Click to view the code for the function `get_labels`</summary>

```python
# Code for the function get_labels
```

</details>

#### delete_all_folders

- <span style="color:green">**Purpose**</span>: Based on the function name, it is likely used to delete all folders in a specified path or perform some cleanup.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: None.

<details>
  <summary>Click to view the code for the function `delete_all_folders`</summary>

```python
# Code for the function delete_all_folders
```

</details>

#### remove_docker_container

- <span style="color:green">**Purpose**</span>: This function is intended to remove a Docker container based on a specified name or ID.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: None.

<details>
  <summary>Click to view the code for the function `remove_docker_container`</summary>

```python
# Code for the function remove_docker_container
```

</details>

#### create_structure

- <span style="color:green">**Purpose**</span>: Creating the main folder directory (with the right name).
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: None.

<details>
  <summary>Click to view the code for the function `create_structure`</summary>

```python
# Code for the function create_structure
```

</details>

#### move_result

- <span style="color:green">**Purpose**</span>: Handles the process of moving results.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: None.

<details>
  <summary>Click to view the code for the function `move_result`</summary>

```python
# Code for the function move_result
```

</details>

#### clean_all

- <span style="color:green">**Purpose**</span>: Load the docker image.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: None.

<details>
  <summary>Click to view the code for the function `clean_all`</summary>

```python
# Code for the function clean_all
```

</details>

#### gpu_available

- <span style="color:green">**Purpose**</span>: Decodes the output and splits it into lines to determine GPU availability.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: Boolean indicating if GPU is available.

<details>
  <summary>Click to view the code for the function `gpu_available`</summary>

```python
# Code for the function gpu_available
```

</details>

#### exec_in_docker

- <span style="color:green">**Purpose**</span>: Executes commands within the Docker container.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: None.

<details>
  <summary>Click to view the code for the function `exec_in_docker`</summary>

```python
# Code for the function exec_in_docker
```

</details>

#### load_image

- <span style="color:green">**Purpose**</span>: Function for the terminal to do image loading.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: None.

<details>
  <summary>Click to view the code for the function `load_image`</summary>

```python
# Code for the function load_image
```

</details>

#### launch_docker

- <span style="color:green">**Purpose**</span>: Handles the process of launching the Docker image.
- <span style="color:blue">**Parameters**</span>: None.
- <span style="color:red">**Returns**</span>: None.

<details>
  <summary>Click to view the code for the function `launch_docker`</summary>

```python
# Code for the function launch_docker
```

</details>

---

### Main Execution

On executing the script:

1. It checks if the input folder exists.
2. If found, it processes the command-line arguments and initiates the image preparation procedure.
3. If not, it exits, indicating the missing folder.

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

