
## Documentation for `exe_transferLearning.py`

---

### Overview

The `exe_transferLearning.py` script is designed for finetune an existing model to make it more accurate.

### Table of Contents

- [Prerequisites](#prerequisites)
- [Main Execution](#main-execution)
- [Functions](#functions)
- [Usage](#usage)

---

### Prerequisites

Ensure you have the following libraries installed:

import time as tm


import delete_all
import generalFunctions

- os
- sys
- argparse
- time as tm

---

### Main Execution
The logics is exactly the same as the [exe_train.md](exe_train.md). The differences are the values of the different variables and, if everything is correct, it will start the "start_process_tl" function from general


<details>
  <summary><strong> Click to view the code for the main execution</strong></summary>

```python
import os
import sys
import argparse
import time as tm


import delete_all
import generalFunctions


"""-----------------------------GLOBAL VARIABLES------------------------------"""
#MAIN PATHS 
main_path = os.path.dirname(os.path.abspath(__file__)) #Get the parent path of the main folder

input_folder_name = "Input_transferLearning"
input_folder_path = os.path.join(main_path, "transferLearning", input_folder_name)

if input_folder_path:
    if len(os.listdir(input_folder_path)) == 0: #This means that the data was not added into the right folder
        print("Input transfer learning folder is empty!")
        sys.exit() 

    elif len(os.listdir(input_folder_path)) > 1: #This case is not possible, just clean everything and stop the process
        delete_all.clean_all(delete_input_folder=True, delete_output_folder=True, delete_model_folder=True, delete_all_nnunet_folder=True, script="transferLearning")
        print("Too many input folders, everything was cleaned, launch the training again!")
        sys.exit()

    else:
        print(f"Found {input_folder_name} at: {input_folder_path}")
        if __name__ == "__main__":
            #Get the values of the input command
            timer_pretraining_start = tm.time()
            parser = argparse.ArgumentParser()
            parser.add_argument("-l", "--label", dest="label", type=int)
            parser.add_argument("-i", "--image_type", dest="image_type", type=str, default= "CT")
            parser.add_argument("-t", "--time", dest="time", type=int, default=60)
            parser.add_argument("-c", "--configuration_model", dest="configuration_model", type=str, default= "3d_fullres")
            args = parser.parse_args()
            label_number = args.label
            image_type = args.image_type
            time_input = args.time
            configuration_model = args.configuration_model

            #Main code to run
            generalFunctions.start_process_tl(timer_pretraining_start, label_number, image_type, time_input, configuration_model)
            
else:
    print(f"{input_folder_name} not found.")
    sys.exit()
```
</details>


---

### Usage 

To execute the `exe_transferLearning.py` script, use the following command:

```
python exe_transferLearning.py [-l LABEL] [-i IMAGE_TYPE] [-t TIME]
```

Arguments:
- `-l` or `--label`: Number of label to be used ().
- `-i` or `--image_type`: Type of image (default: "CT").
- `-t` or `--time`: Time parameter (default: 60).


