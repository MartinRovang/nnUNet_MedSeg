# Running the Python Script with a New Dataset

Training a model on a custom dataset is essential, especially for tasks that require specialized data. In this section, users are guided step-by-step on how to set up and train a new model using their dataset.

## Dataset Preparation

Before starting, users should:

1. Make sure the dataset aligns with the stipulated [format](dataset_format.md).
2. Then, copy this well-formatted dataset into the `input_nnUNet_train` folder.

## Initiating the Training Process

To begin, simply [execute](training.md#command-execution) the `exe_train.py` script. When executed, the script undergoes several stages:

- **Data Sorting Stage**: At this point, data labeled as 'validate' or 'train' gets selected for the training process.
  
  - The script sorts and classifies the data into two distinct folders: 
    - `imagesTr`: This is where all the images are stored.
    - `labelsTr`: This section is reserved for labels or filters.
  
  Additionally, a JSON file is generated. This file captures specific information that users specify during the command-line execution. All of these elements (folders and files) are neatly placed within the `raw_nnUNet` directory.

- **Preprocessing Stage**: The nnUNet model takes the lead here. The data undergoes a `3d_fullres` preprocessing
  
- **Training Stage**: At this point, the script scouts for available GPUs. Once it identifies an available unit, it immediately begin the training on that GPU. **(In the code it is fixed that the choosed GPU will by the 0)**
  - **Important Note**: In cases where no GPUs are available, the script halts the training process. As a result, data gets deleted, and users will need to restart the process once a GPU becomes available.

A word of caution: Timing is pivotal. If the script runs out of the designated time before completing the preprocessing, it stops abruptly. In such cases, all data is purged. Therefore, users must ensure that they allocate sufficient time for the process to run its course.

Upon the successful completion of training—whether it reaches the predetermined time cap—the results are saved in the `output_nnUNet_train` folder. Within this directory, users will find a file named after the dataset. This file contains only the essential files required to use the model for predictions.

It's important to note that the nnUNet folders are locked against modifications to guarantee smooth progression through all steps.

