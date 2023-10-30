
## Documentation for `exe_train.py`

----------

### Overview

The `exe_train.py` script is designed for processing and preparing NIfTI (.nii) images for the nnUNet framework, a renowned deep learning framework for biomedical image segmentation.

### Table of Contents

- [Prerequisites](#prerequisites)
- [Functions](#functions)
- [Main Execution](#main-execution)
- [Usage](#usage)

----------

### Prerequisites

Ensure you have the following libraries installed:
- os
- sys
- time as tm
- argparse

- delete_all (python script)
- generalFunctions (python script)
  

----------

### Main Execution 

1. Definition of all the different needed path for the process and the global variables
2. Checks if the input folder exists
3. If found, 3 different cases might happen:
  - 0 folder inside the input folder. This means that the data is not placed correctly, the code stops.
  - More than 1 folder is found. This means that there are too many folder. The function clean_all from delete_all.py is called to clean up all the folders and then stops the code.
  - Only 1 folder is found. The code continues correctly, all the global variables are definied in respect with the values of the flags of the command line. Finally, the function "start_process_training" from generalFunctions starts.
4. If not found, the code stops and indicates the missing folder

<details>
  <summary><strong> Click to view the code for the main execution</strong></summary>

```python
"""-----------------------------IMPORT------------------------------"""
import os
import sys
import argparse
import time as tm

import delete_all
import generalFunctions


"""-----------------------------GLOBAL VARIABLES------------------------------"""
#MAIN PATHS 
input_folder_name = "Input_nnUNet_train"

main_path = os.path.dirname(os.path.abspath(__file__)) #Get the parent path of the main folder
input_folder_path = os.path.join(main_path, "train", input_folder_name)


if input_folder_path:
    if len(os.listdir(input_folder_path)) == 0: #This means that the data was not added into the right folder
        print("Input folder is empty!")
        sys.exit() 

    elif len(os.listdir(input_folder_path)) > 1: #This case is not possible, just clean everything and stop the process
        delete_all.clean_all(delete_input_folder=True, delete_output_folder=True, delete_model_folder=False, delete_all_nnunet_folder=True, script = "train")
        print("Too many input folders, everything was cleaned, launch the training again!")
        sys.exit()

    else:
        print(f"Found {input_folder_name} at: {input_folder_path}")
        delete_all.clean_all(delete_input_folder=False, delete_output_folder=True, delete_model_folder=False, delete_all_nnunet_folder=False, script = "train") #To clean everything up in case something went wrong before
        #Get the values of the input command
        timer_training_start = tm.time()
        parser = argparse.ArgumentParser()
        parser.add_argument("-d", "--dataset_name", dest="dataset_name", type=str, default="No_Name")
        parser.add_argument("-l", "--label", dest="label", type=int)
        parser.add_argument("-i", "--image_type", dest="image_type", type=str, default= "CT")
        parser.add_argument("-t", "--time", dest="time", type=int, default=60)
        parser.add_argument("-c", "--configuration_model", dest="configuration_model", type=str, default= "3d_fullres")
        args = parser.parse_args()
        dataset_name = args.dataset_name
        label_number = args.label
        image_type = args.image_type
        time_input = args.time
        configuration_model = args.configuration_model

        #Main code to run
        generalFunctions.start_process_training(timer_training_start, dataset_name, label_number, image_type, time_input, configuration_model)
            
else:
    print(f"{input_folder_name} not found.")
    sys.exit()
```
</details>

---


### Usage

To run the script, use:

```bash
python exe_train.py -d [DATASET_NAME] -l [LABEL] -i [IMAGE_TYPE] -t [TIME] -c [CONFIGURATION_MODEL]
```

- `-d, --dataset_name`: Name of the dataset (default: "No_Name").
- `-l, --label`: Label number to retain in the image.
- `-i, --image_type`: Type of the image (default: "CT").
- `-t, --time`: Time parameter (default: 60).
- `-c, --configuration_model`: Configuration (default: 3d_fullres).

---


