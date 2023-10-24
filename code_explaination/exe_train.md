
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

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Determines if the provided directory contains images designated for training or validation.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `directory` (str): Path to the directory to check.
- ![Returns](https://img.shields.io/badge/-Returns-red): 
  - `True` if training or validation images are found.
  - `False` otherwise.

<details>
  <summary>Click to view the code for the function `check_for_train_or_validate`</summary>

```python
# Code for the function check_for_train_or_validate
def check_for_train_or_validate(directory):
    for filename in os.listdir(directory): #List all the files in the folder
        if filename.startswith('train.') or filename.startswith('validate.'): #Check if the name starts with "train" or "validate"
            return True
    return False
```

</details>

#### process_image

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Processes a NIfTI image to retain only a specified label.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `input_filename_path` (str): Path to the input image.
  - `output_filename_path` (str): Path to save the processed image.
- ![Returns](https://img.shields.io/badge/-Returns-red): None. The processed image is saved to the specified path.

<details>
  <summary>Click to view the code for the function `process_image`</summary>

```python
# Code for the function process_image
def process_image(input_filename_path, output_filename_path):
    image = sitk.ReadImage(input_filename_path) # Load the nifti image
    output_image = sitk.Threshold(image, lower=0, upper=label_number, outsideValue=0) # Threshold the image: values above label_number (global variable definied in a flag) are set to 0, all other values remain unchanged
    sitk.WriteImage(output_image, output_filename_path)
```

</details>

#### get_channel_names

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

#### get_labels

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

#### create_split_json

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Constructs a JSON structure denoting training and validation splits.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `train_list` (list): List of training images.
  - `val_list` (list): List of validation images.
- ![Returns](https://img.shields.io/badge/-Returns-red): None. The JSON structure is saved in the appropriate directory.


<details>
  <summary>Click to view the code for the function `create_split_json`</summary>

```python
# Code for the function create_split_json
```

</details>

#### get_labels

- ![Purpose](https://img.shields.io/badge/-Purpose-green): This function appears to be designed to retrieve labels for the nnUNet JSON structure. Based on the provided label number, it generates a dictionary of labels.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): A dictionary with label names and their corresponding indices.

<details>
  <summary>Click to view the code for the function `get_labels`</summary>

```python
# Code for the function get_labels
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

#### create_structure

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Creating the main folder directory (with the right name).
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): None.

<details>
  <summary>Click to view the code for the function `create_structure`</summary>

```python
# Code for the function create_structure
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

#### clean_all

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Load the docker image.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): None.
- ![Returns](https://img.shields.io/badge/-Returns-red): None.

<details>
  <summary>Click to view the code for the function `clean_all`</summary>

```python
# Code for the function clean_all
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

