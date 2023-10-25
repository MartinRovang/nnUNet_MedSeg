
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

The script starts by defining the main paths and necessary variables. It then checks if the input folder contains data for prediction. If data is present, it initiates the prediction using Docker and the nnUNet model. After the prediction, it cleans up temporary folders and displays a message indicating that the prediction is done.

---

### Functions

:point_right: **list_model_available** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Displays all available models in the specified folder.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

```python
def list_model_available():
    print("All models available:")
    for folder in os.listdir(model_folder_path_result):
        print(f"{folder}")
```

---

:point_right: **create_folder** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Creates the necessary folders for input and output, and copies the input files and models to the appropriate folders.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

---

:point_right: **remove_folder** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Removes all temporary folders and unnecessary files after prediction.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

---

:point_right: **get_dataset_name** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Gets the dataset name from the model name.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) `str`: The name of the dataset.

---

:point_right: **get_fold_value** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Gets the fold value from the model folder.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) `str`: The fold value.

---

:point_right: **extract_values** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Extracts necessary values from a file.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `file_path` (str): Path to the file to be read.
- ![Returns](https://img.shields.io/badge/-Returns-red) `tuple`: The extracted values.

---

:point_right: **remove_docker_container** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Removes a Docker container using its ID.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `id` (str): The ID of the Docker container to remove.
- ![Returns](https://img.shields.io/badge/-Returns-red) None

---

:point_right: **gpu_available** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Checks for available GPUs for Docker.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) `list`: Indices of available GPUs.

---

:point_right: **exec_in_docker** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Executes a command within the Docker container.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `cmd` (str): The command to execute.
- ![Returns](https://img.shields.io/badge/-Returns-red) None

---

:point_right: **load_image** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Loads a Docker image.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

---

:point_right: **launch_docker_prediction** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Launches the prediction using Docker and the nnUNet model.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) None
- ![Returns](https://img.shields.io/badge/-Returns-red) None

---

### Usage

To use this script, place your input data in the specified folder and run the script. Ensure that all dependencies are installed and Docker is properly configured on your machine.
