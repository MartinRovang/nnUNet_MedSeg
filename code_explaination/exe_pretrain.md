
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

### Main execution







---

### Functions

#### check_for_train_or_validate

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Checks if there's a file named 'train.*' or 'validate.*' in the directory.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `directory`: Path or directory
  - `directory`: Description to be added.
- ![Returns](https://img.shields.io/badge/-Returns-red): Returns a value.

<details>
  <summary>Click to view the code for the function `check_for_train_or_validate`</summary>

```python
# Code for the function check_for_train_or_validate
```

</details>

#### process_image

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `input_filename_path`: Path or directory
  - `output_filename_path`: Path or directory
  - `input_filename_path`: Description to be added.
  - `output_filename_path`: Description to be added.
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `process_image`</summary>

```python
# Code for the function process_image
```

</details>

#### get_model_name

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Retrieves necessary components related to get_model_name.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `get_model_name`</summary>

```python
# Code for the function get_model_name
```

</details>

#### get_fold_value

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Retrieves necessary components related to get_fold_value.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
- ![Returns](https://img.shields.io/badge/-Returns-red): Returns a value.

<details>
  <summary>Click to view the code for the function `get_fold_value`</summary>

```python
# Code for the function get_fold_value
```

</details>

#### remove_folder_model

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `remove_folder_model`</summary>

```python
# Code for the function remove_folder_model
```

</details>

#### list_new_data

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `data_tot_path`: Path or directory
  - `data_tot_path`: Description to be added.
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `list_new_data`</summary>

```python
# Code for the function list_new_data
```

</details>

#### new_json

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `new_json`</summary>

```python
# Code for the function new_json
```

</details>

#### copy_json_file

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `copy_json_file`</summary>

```python
# Code for the function copy_json_file
```

</details>

#### create_split_json

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Creates and sets up necessary components for the create_split_json.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `create_split_json`</summary>

```python
# Code for the function create_split_json
```

</details>

#### get_channel_names

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Retrieves necessary components related to get_channel_names.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
- ![Returns](https://img.shields.io/badge/-Returns-red): Returns a value.

<details>
  <summary>Click to view the code for the function `get_channel_names`</summary>

```python
# Code for the function get_channel_names
```

</details>

#### get_labels

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Retrieves necessary components related to get_labels.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
- ![Returns](https://img.shields.io/badge/-Returns-red): Returns a value.

<details>
  <summary>Click to view the code for the function `get_labels`</summary>

```python
# Code for the function get_labels
```

</details>

#### create_structure

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Creates and sets up necessary components for the create_structure.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
- ![Returns](https://img.shields.io/badge/-Returns-red): Returns a value.

<details>
  <summary>Click to view the code for the function `create_structure`</summary>

```python
# Code for the function create_structure
```

</details>

#### move_result

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `move_result`</summary>

```python
# Code for the function move_result
```

</details>

#### delete_all_folders

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `path_folder`: Path or directory
  - `docker_path`: Path or directory
  - `path_folder`: Description to be added.
  - `docker_path`: Description to be added.
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `delete_all_folders`</summary>

```python
# Code for the function delete_all_folders
```

</details>

#### remove_docker_container

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `id`: Variable
  - `id`: Description to be added.
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `remove_docker_container`</summary>

```python
# Code for the function remove_docker_container
```

</details>

#### clean_all

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `clean_all`</summary>

```python
# Code for the function clean_all
```

</details>

#### gpu_available

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Returns a value.

<details>
  <summary>Click to view the code for the function `gpu_available`</summary>

```python
# Code for the function gpu_available
```

</details>

#### exec_in_docker

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - `cmd`: Variable
  - `cmd`: Description to be added.
- ![Returns](https://img.shields.io/badge/-Returns-red): Returns a value.

<details>
  <summary>Click to view the code for the function `exec_in_docker`</summary>

```python
# Code for the function exec_in_docker
```

</details>

#### creation_checkpoint_folder

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `creation_checkpoint_folder`</summary>

```python
# Code for the function creation_checkpoint_folder
```

</details>

#### load_image

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `load_image`</summary>

```python
# Code for the function load_image
```

</details>

#### launch_docker

- ![Purpose](https://img.shields.io/badge/-Purpose-green): Description to be added.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue): 
  - None
- ![Returns](https://img.shields.io/badge/-Returns-red): Doesn't return a value.

<details>
  <summary>Click to view the code for the function `launch_docker`</summary>

```python
# Code for the function launch_docker
```

</details>

### Usage

To execute the `exe_pretrain.py` script, use the following command:

```
python exe_pretrain.py [-l LABEL] [-i IMAGE_TYPE] [-t TIME]
```

Arguments:
- `-l` or `--label`: Label to be used (default: "TUMOR").
- `-i` or `--image_type`: Type of image (default: "CT").
- `-t` or `--time`: Time parameter (default: 60).


