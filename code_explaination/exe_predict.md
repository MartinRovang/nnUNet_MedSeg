
## Documentation for `exe_predict.py`

---

### Overview

The `exe_predict.py` script is designed to perform predictions using a deep learning model with the nnUNet model. It takes images as input, processes them through a trained model, and produces the prediction results.

### Table of Contents

- [Prerequisites](#prerequisites)
- [Main Execution](#main-execution)
- [Functions](#functions)
- [Usage](#usage)

---

### Prerequisites

Ensure you have the following libraries installed:

- os
- sys
- shutil
- subprocess
- re
- delete_all
- generalFunctions

---

### Main Execution


---

### Functions

:point_right: **list_model_available( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Displays all available models in the specified folder.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red)
  - print all the models available

<details>
  <summary>Click to view the code for the function `list_model_available( )`</summary>

```python
# Code for the function process_image
```

</details>

##  

:point_right: **create_folder( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates the necessary folders, copies the input files and models into the appropriate folders.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `create_folder( )`</summary>

```python
# Code for the function process_image
```

</details>

##  


:point_right: **get_dataset_name( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Gets the dataset name from the model name.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red)
 - `folder`(str): The name of the dataset.

<details>
  <summary>Click to view the code for the function `get_dataset_name( )`</summary>

```python
# Code for the function process_image
```

</details>

##  

:point_right: **get_fold_value( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Gets the fold value from the model folder.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red)
 - `folder.split("_")[1]`(str): The fold value.

<details>
  <summary>Click to view the code for the function `get_fold_value( )`</summary>

```python
# Code for the function process_image
```

</details>

##  

:point_right: **extract_values(file_path)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Extracts necessary values from a file to get the right command line. (Find best configuration) Not used.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `file_path` (str): Path to the file to be read.
- ![Returns](https://img.shields.io/badge/-Returns-red)
  - `f_value, tr_value, c_value, p_value` (tuple): The extracted values for the command line.

<details>
  <summary>Click to view the code for the function `extract_value(file_path)`</summary>

```python
# Code for the function process_image
```

</details>

##  


:point_right: **launch_docker_prediction( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Handles the process of launching the Docker image
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `launch_docker_prediction( )`</summary>

```python
# Code for the function process_image
```

</details>

---  

### Usage

To execute the `exe_predict.py` script, use the following command:

```
python exe_predict.py 
```

