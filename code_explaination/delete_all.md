## Documentation for `delete_all.py`

---

### Overview

The `delete_all.py` script is designed to delete and clean all the folders in the Docker

### Table of Contents

- [Prerequisites](#prerequisites)
- [Main Execution](#main-execution)
- [Functions](#functions)
- [Usage](#usage)

---

### Prerequisites

Ensure you have the following libraries installed:

- os
- subprocess
- globalPath

---

### Main Execution


---

### Functions

:point_right: **exec_in_docker(cmd, container_id)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) 
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
   - `cmd`(str):
   - `container_id` (int??): 
- ![Returns](https://img.shields.io/badge/-Returns-red)
  - reslut

<details>
  <summary>Click to view the code for the function `exec_in_docker(cmd, container_id)`</summary>

```python
def exec_in_docker(cmd, container_id):
    exec_command = f"docker exec -i {container_id} bash -c '{cmd}'"
    result = subprocess.call(exec_command, shell=True)
    return result
```

</details>

##



:point_right: **delete_all_folders(path_folder, docker_path)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) 
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
   - `cmd`(str):
   - `container_id` (int??): 
- ![Returns](https://img.shields.io/badge/-Returns-red)
  - reslut

<details>
  <summary>Click to view the code for the function `delete_all_folders(path_folder, docker_path)`</summary>

```python
def delete_all_folders(path_folder, docker_path):
    print(f"Deleting folders in {docker_path} as seen from Docker...")
    for folder in os.listdir(path_folder):
        print(f"Attempting to delete {folder}...")
        command = f"rm -r {os.path.join(docker_path, folder)}"
        result = exec_in_docker(command, container_id)
        if result == 0:
            print(f"Successfully deleted {folder}.")
        else:
            print(f"Failed to delete {folder}.")
```

</details>

##  

:point_right: **clean_all(delete_input_folder, delete_output_folder, delete_model_folder, delete_all_nnunet_folder, script)** :point_left:

- ![Purpose](https://img.shields.io/badge/-Purpose-green) 
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
   - `cmd`(str):
   - `container_id` (int??): 
- ![Returns](https://img.shields.io/badge/-Returns-red)
  - reslut

<details>
  <summary>Click to view the code for the function `clean_all(delete_input_folder, delete_output_folder, delete_model_folder, delete_all_nnunet_folder, script)`</summary>

```python
def clean_all(delete_input_folder, delete_output_folder, delete_model_folder, delete_all_nnunet_folder, script):
    global container_id
        
    #Once the training is done, it will delete all the created folders!
    docker_command = f"docker run -d -it --gpus all --shm-size 8g -v {main_path}:/app/nnUNet {image_docker} bash"
    container_id = subprocess.check_output(docker_command, shell=True).decode().strip()

    globalPath.myPath(script) #To have the right value for the different paths
    
    if delete_input_folder: #Delete only if the value is TRUE!
        delete_all_folders(globalPath.input_folder_path, globalPath.docker_nnunet_input_path)

    if delete_output_folder: #Delete only if the value is TRUE!
        delete_all_folders(globalPath.output_folder_path, globalPath.docker_nnunet_output_path)

    if script == "transferLearning" and delete_model_folder: #Only for the transferLearning!
        delete_all_folders(globalPath.model_folder_path, globalPath.docker_model_path)

    if delete_all_nnunet_folder:
        delete_all_folders(globalPath.nnunet_preprocessed_path, globalPath.docker_nnunet_preprocessed_path)
        delete_all_folders(globalPath.nnunet_result_path, globalPath.docker_nnunet_result_path)
        delete_all_folders(globalPath.nnunet_raw_path, globalPath.docker_nnunet_raw_path)

    

    global_commands = f"docker stop {container_id}"
    subprocess.check_output(global_commands, shell=True, stderr=subprocess.STDOUT)

    global_commands = f"docker rm {container_id}"
    subprocess.check_output(global_commands, shell=True, stderr=subprocess.STDOUT)

    print(f"Docker container id: {container_id} has been removed")
    print("Deletion completed")
```

</details>

##  

### Usage

This function is used in [generalFunctions](generalFunctions), [exe_train](exe_train.md), [exe_predict](exe_predict.md), and [exe_transferLearning](exe_transferLearning.md) whenever there is a need to remove and clean specific folders. It is called at the end of each step or in instances where an issue arises.

