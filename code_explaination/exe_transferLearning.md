
## Documentation for `exe_transferLearning.py`

---

### Overview

The `exe_transferLearning.py` script is designed for finetune an existing model to make it more accurate.

### Table of Contents

- [Prerequisites](#prerequisites)
- [Variables](#variables)
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
### Variables

---

### Main Execution


---

### Functions


:point_right: **Get_fold_value( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Check the fold value.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - Path to the `fold` folder 
- ![Returns](https://img.shields.io/badge/-Returns-red) return the folder value

<details>
  <summary>Click to view the code for the function `Get_fold_value( )`</summary>

```python
# Code for the function get_fold_value
```

</details>

##  

:point_right: **Remove_folder_model( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Delete the content of `model` folder 
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  -  `model_folder_path` (str): path to the `model` folder.
- ![Returns](https://img.shields.io/badge/-Returns-red) None.

<details>
  <summary>Click to view the code for the function `Remove_folder_model( )`</summary>

```python
# Code for the function remove_folder_model
```

</details>

##  

:point_right: **List_new_data(data_tot_path)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Sort the data into 'val' and 'train', keep previous data in the original split
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
  - `data_tot_path`(str): Path or directory
- ![Returns](https://img.shields.io/badge/-Returns-red)
  -?????????????????

<details>
  <summary>Click to view the code for the function `List_new_data( )`</summary>

```python
# Code for the function list_new_data
```

</details>

##  

:point_right: **New_json( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Write a new JSON file with the right split
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `New_json( )`</summary>

```python
# Code for the function new_json
```

</details>

##  

:point_right: **Copy_json_file( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Copy the JSON file in the right folder
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red)
  - Copied the JSON file into `splits_final.json`

<details>
  <summary>Click to view the code for the function `Copy_json_file( )`</summary>

```python
# Code for the function copy_json_file
```

</details>

##  

:point_right: **Create_split_json( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates and sets up necessary components for the `create_split_json`
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `Create_split_json( )`</summary>

```python
# Code for the function create_split_json
```

</details>
 
##  

:point_right: **Creation_checkpoint_folder( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Copy of the `model` folder into the `dataset_source_name` folder in `nnunet_result_path`
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `Creation_checkpoint_folder( )`</summary>

```python
# Code for the function creation_checkpoint_folder
```

</details>

##  
 

:point_right: **Launch_docker( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Handles the process of launching the Docker image
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `Launch_docker( )`</summary>

```python
# Code for the function launch_docker
```

</details>

---

### Usage 

To execute the `exe_transferLearning.py` script, use the following command:

```
python exe_transferLearning.py [-l LABEL] [-i IMAGE_TYPE] [-t TIME]
```

Arguments:
- `-l` or `--label`: Label to be used (default: "TUMOR").
- `-i` or `--image_type`: Type of image (default: "CT").
- `-t` or `--time`: Time parameter (default: 60).


