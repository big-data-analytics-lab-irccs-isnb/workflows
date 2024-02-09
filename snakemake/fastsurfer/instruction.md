# Fastsurfer

Run the whole Fastsurfer + Freesurfer pipeline on all the specified T1 - weighted MRI. 

## Requirements

This pipeline requires Fastsurfer and freesurfer to be installed on your system.
Please find [here]() the instruction to install fastsurfer and [here]() the one to install freesurfer.
**Note** Fastsurfer requires a specific version of freesurfer to work with. 
Please ensure to have the correct version installed before running the workflow.


## Usage

To run the workflow you have to follow these steps

1. [List of image creation](#List_of_image_creation)
2. [Workflow Configuration](#Workflow_Configuration)
3. [Workflow Running](Workflow_Running)


### List of image creation

The first step is the creation of a file .txt with the relative path to the folder containing 
each T1-weighted image to be processed by FastSurfer.

To given an example, suppose to have the data organized as follows:

```
    ├── patient_1
    │   ├── study_1
    │   │   ├── anat
    |   |   |   ├── t1.nii
    ├── patient_2
    │   ├── study_1
    │   │   ├── anat
    |   |   |   ├── t1.nii
    │   ├── study_2
    │   │   ├── anat
    |   |   |   ├── t1.nii
    ├── patient_3
    │   ├── study_1
    │   │   ├── anat
    |   |   |   ├── t1.nii

```

Than the text file should read as


patient_1/study_1/anat
patient_2/study_1/anat
patient_2/study_2/anat
patient_3/study_1/anat

**Note** The target t1 image should be named *t1.nii*. 

The final FastSurfer Segmentation will be saved in a folder called fastsurfer at the same level of the anat folder

```

    ├── patient_1
    │   ├── study_1
    │   │   ├── anat
    |   |   |   ├── t1.nii
    │   |   ├── fastsurfer
```

### Workflow Configuration

The second step should be the filling of the config.yaml file. 
The field to fill are the follows:

- **fastsurfer_path**: path to the directory containing the file.
- **fastsurfer_environment_path**: path to the .yaml file containing the conda environment specification for FastSurfer
- **basepath**: path to the folder containing the patient data; i.e. the path to the t1 must be: basepath/patient_1/study_1/anat/t1.nii
- **series_path**: path the .txt file described above.

### Workflow Running


TO run the workflow you have to activate the snakemake conda environment
```shell
conda activate snakemake
```

and then run the following command

```
snakemame -j8 --use-conda --rerun-incomplete
```

Where:
-  -j8 specify the number of jobs to be executed in parallel, so adjust it according to your needind


### Prepare the list of patient to be processed


### Configure the snakemake pipeline

To use the snakemake workflow simply set the following config parameters in the config.yaml file 

- **fastsurfer_path** : path to the directory containing the *run_fastsurfer.sh* script.
- **base_path**: 
- **output_path**: path to the output directory
- **list_of_series**:
- **fastsurfer_environment_path**: path to the .yaml file where the conda environment for fastsurfer is specified.


## Run the snakemake pipeline
