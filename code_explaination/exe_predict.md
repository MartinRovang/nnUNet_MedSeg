
## Documentation for `script_python.py`

---

### Overview

The `script_python.py` script is designed to perform predictions using a deep learning model with the nnUNet library. It takes images as input, processes them through a pre-trained model, and produces the prediction results.

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
- argparse
- subprocess
- re

---

### Main Execution


---

### Functions

:point_right: **list_model_available( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Displays all available models in the specified folder.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) 
- ![Returns](https://img.shields.io/badge/-Returns-red) Print all the models available

<details>
  <summary>Click to view the code for the function `list_model_available()`</summary>

```python
# Code for the function process_image
```

</details>

##  

:point_right: **create_folder( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates the necessary folders for input and output, and copies the input files and models to the appropriate folders.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `create_folder()`</summary>

```python
# Code for the function process_image
```

</details>

##  


:point_right: **get_dataset_name( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Gets the dataset name from the model name.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) `str`: The name of the dataset.

<details>
  <summary>Click to view the code for the function `get_dataset_name()`</summary>

```python
# Code for the function process_image
```

</details>

##  

:point_right: **get_fold_value( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Gets the fold value from the model folder.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) `str`: The fold value.

<details>
  <summary>Click to view the code for the function `get_fold_value()`</summary>

```python
# Code for the function process_image
```

</details>

##  

:point_right: **extract_values(file_path)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Extracts necessary values from a file to get the right command line. (Find best configuration) Not used.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `file_path` (str): Path to the file to be read.
- ![Returns](https://img.shields.io/badge/-Returns-red) `tuple`: The extracted values.

<details>
  <summary>Click to view the code for the function `extract_value(file_path)`</summary>

```python
# Code for the function process_image
```

</details>

##  


:point_right: **launch_docker_prediction( )** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Launches the prediction using Docker and the nnUNet model.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

<details>
  <summary>Click to view the code for the function `launch_docker_prediction()`</summary>

```python
# Code for the function process_image
```

</details>

##  

:point_right:Usage:point_left:

To execute the `exe_predict.py` script, use the following command:

```
python exe_predict.py 
```

