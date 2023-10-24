
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

- **Purpose**: """Checks if there's a file named 'train.*' or 'validate.*' in the directory."""
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `check_for_train_or_validate`</summary>

```python
# Code for the function check_for_train_or_validate
```

</details>

#### process_image

- **Purpose**: # Load the nifti image
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `process_image`</summary>

```python
# Code for the function process_image
```

</details>

#### get_channel_names

- **Purpose**: # num_channels = int(input("Enter number of channels: ")) #Uncomment for multichannel
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `get_channel_names`</summary>

```python
# Code for the function get_channel_names
```

</details>

#### get_labels

- **Purpose**: No description provided.
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `get_labels`</summary>

```python
# Code for the function get_labels
```

</details>

#### create_split_json

- **Purpose**: #------------------------------FOLDERS + JSON FILE + MOVING IMAGES------------------------------
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `create_split_json`</summary>

```python
# Code for the function create_split_json
```

</details>

#### get_labels

- **Purpose**: No description provided.
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `get_labels`</summary>

```python
# Code for the function get_labels
```

</details>

#### delete_all_folders

- **Purpose**: No description provided.
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `delete_all_folders`</summary>

```python
# Code for the function delete_all_folders
```

</details>

#### remove_docker_container

- **Purpose**: No description provided.
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `remove_docker_container`</summary>

```python
# Code for the function remove_docker_container
```

</details>

#### create_structure

- **Purpose**: #Creating the main folder directory (with the right name)
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `create_structure`</summary>

```python
# Code for the function create_structure
```

</details>

#### move_result

- **Purpose**: #------------------------------TERMINAL------------------------------
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `move_result`</summary>

```python
# Code for the function move_result
```

</details>

#### clean_all

- **Purpose**: #Load the docker image
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `clean_all`</summary>

```python
# Code for the function clean_all
```

</details>

#### gpu_available

- **Purpose**: # Decode the output and split it into lines
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `gpu_available`</summary>

```python
# Code for the function gpu_available
```

</details>

#### exec_in_docker

- **Purpose**: # Execute commands within the Docker container
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `exec_in_docker`</summary>

```python
# Code for the function exec_in_docker
```

</details>

#### load_image

- **Purpose**: #Function for the terminal to do
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `load_image`</summary>

```python
# Code for the function load_image
```

</details>

#### launch_docker

- **Purpose**: #Loading the docker image
- **Parameters**: 
  - To be determined based on the function.
- **Returns**: 
  - To be determined based on the function.

<details>
  <summary>Click to view the code for the function `launch_docker`</summary>

```python
# Code for the function launch_docker
```

</details>
