## Documentation for `delet_all.py`

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
  <summary>Click to view the code for the function `exec_in_docker(cmd, container_id)`:summary>

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
  <summary>Click to view the code for the function `delete_all_folders(path_folder, docker_path)`:summary>

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
  <summary>Click to view the code for the function `clean_all(delete_input_folder, delete_output_folder, delete_model_folder, delete_all_nnunet_folder, script)`:summary>

```python
def exec_in_docker(cmd, container_id):
    exec_command = f"docker exec -i {container_id} bash -c '{cmd}'"
    result = subprocess.call(exec_command, shell=True)
    return result
```

</details>

##  
