# Training with nnUNet

Training is pivotal as it lays the foundation for building an efficient 3D segmentation model using nnUNet.

## Using nnUNet_medseg

To ensure the optimal utilization of the `nnUNet_medseg` program and prevent data loss, users should adhere to the provided guidelines.

### Training Scenarios

3 primary use-cases can be achieved with this program:

1. [New Dataset Training](train_new_dataset.md): Train from scratch using an entirely new dataset. (Most common use-case)
2. **Parameter Variation**: Re-train on the same dataset but with varied parameters.
3. [Leveraging Pre-trained Models](pretrained_model.md): Make use of an existing pre-trained model.

### User Interaction

Users will primarily engage with the `Input_nnUNet_train`, `exe_train.py`, and its output counterpart. It's imperative to ⚠️**COPY**⚠️ the dataset into `Input_nnUNet_train`. The program will sort the dataset for the nnUNet model and then delete it post-operation. Post-training, users will receive an output containing the trained model. All other data will be ⚠️**DELETED**⚠️.

### Command Execution

To correctly deploy `exe_train.py`, use the following command:

```bash
python3 FULL_PATH/exe_train.py -d DATASET_NAME -l LABEL -i IMAGE_TYPE -t TIME -f FOLD -e IMAGE_EXTENSION
```
<details>
  <summary>Click here to have the full name </summary>

```bash
python3 FULL_PATH/exe_train.py --dataset_name DATASET_NAME --label LABEL --image_type IMAGE_TYPE --time TIME --fold FOLD --image_extension IMAGE_EXTENSION
```
 
 <details>
   
- `FULL_PATH`: Don't forget to use the full path to the exe_train.py
- `DATASET_NAME`: Name of your dataset. (**default value**: No_Name)
- `LABEL`: Desired segmentation label (e.g., TUMOR). (**default value**: NONE)
- `IMAGE_TYPE`: Biomedical image variety (e.g., CT, MRI). (**default value**:NONE)
- `TIME`: Desired duration of all the process in MINUTE. (**default value**: 60)
- `FOLD`: Specifies the training fold (maximum of 5 folds). Use "all" to train on every fold for a robust model. (**default value**: all)
- `IMAGE_EXTENSION`: Default is `.nii.gz`. Modify if using a different image extension. 

**Note**: Default values are in place for all parameters and will be employed if a user omits specific arguments. Training caps at 10,000 epochs. However, to ensure efficiency, a time parameter is introduced. If time elapses during an ongoing epoch, the epoch will finalize before terminating the training process.
