
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

- **Purpose**: Determines if the provided directory contains images designated for training or validation.
- **Parameters**: 
  - `directory` (str): Path to the directory to check.
- **Returns**: 
  - `True` if training or validation images are found.
  - `False` otherwise.

#### process_image

- **Purpose**: Processes a NIfTI image to retain only a specified label.
- **Parameters**: 
  - `input_filename_path` (str): Path to the input image.
  - `output_filename_path` (str): Path to save the processed image.
- **Returns**: None. The processed image is saved to the specified path.

#### get_channel_names

- **Purpose**: Fetches channel names required for the nnUNet JSON structure.
- **Parameters**: None.
- **Returns**: 
  - A dictionary with channel names.

#### get_labels

- **Purpose**: Retrieves labels for the nnUNet JSON structure.
- **Parameters**: None.
- **Returns**: 
  - A dictionary with label names and their corresponding indices.

#### create_split_json

- **Purpose**: Constructs a JSON structure denoting training and validation splits.
- **Parameters**: 
  - `train_list` (list): List of training images.
  - `val_list` (list): List of validation images.
- **Returns**: None. The JSON structure is saved in the appropriate directory.


#### get_labels

- **Purpose**: This function appears to be designed to retrieve labels for the nnUNet JSON structure. Based on the provided label number, it generates a dictionary of labels.
- **Parameters**: None.
- **Returns**: A dictionary with label names and their corresponding indices.

#### delete_all_folders

- **Purpose**: Based on the function name, it is likely used to delete all folders in a specified path or perform some cleanup.
- **Parameters**: None.
- **Returns**: None.

#### remove_docker_container

- **Purpose**: This function is intended to remove a Docker container based on a specified name or ID.
- **Parameters**: None.
- **Returns**: None.

#### create_structure

- **Purpose**: Creating the main folder directory (with the right name).
- **Parameters**: None.
- **Returns**: None.

#### move_result

- **Purpose**: Handles the process of moving results.
- **Parameters**: None.
- **Returns**: None.

#### clean_all

- **Purpose**: Load the docker image.
- **Parameters**: None.
- **Returns**: None.

#### gpu_available

- **Purpose**: Decodes the output and splits it into lines to determine GPU availability.
- **Parameters**: None.
- **Returns**: Boolean indicating if GPU is available.

#### exec_in_docker

- **Purpose**: Executes commands within the Docker container.
- **Parameters**: None.
- **Returns**: None.

#### load_image

- **Purpose**: Function for the terminal to do image loading.
- **Parameters**: None.
- **Returns**: None.

#### launch_docker

- **Purpose**: Handles the process of launching the Docker image.
- **Parameters**: None.
- **Returns**: None.

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
