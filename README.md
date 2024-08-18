# QSIPrep_QA_Guide
This is a guide for reviewing QSIPrep's dmri preproc visual quality assessment report html.

First, here is the [official documentation](https://qsiprep.readthedocs.io/en/latest/) for QSIPrep, and here is the nature method [paper](https://www.nature.com/articles/s41592-021-01185-5) that describe the dmri data processing pipeline.

Shortly, qsiprep configures pipelines for processing diffusion-weighted MRI (dMRI) data. The main features of this software are
- A BIDS-app approach to preprocessing diffusion MRI data.
- Automatical preprocessing pipelines that correctly group, distortion correct, motion correct, denoise, coregister and resample your scans, producing visual reports and QC metrics.
- A system for running state-of-the-art reconstruction pipelines that include algorithms from Dipy, MRTrix, DSI Studio and others.
- A novel motion correction algorithm that works on DSI and random q-space sampling schemes

The output of preprocessing from QSIPrep is structured as:
```
Result_dir
├── dataset_description.json
├── dwiqc.json 
├── sub-01.html # Visual quality assessment reports per subject
├── sub-02.html
└── logs
└── sub-01
     ├──  anat  #preproced anat data, cross session
     ├──  figures #preproc figure in the html
     ├──  log
     ├──  ses-HBNsiteRU #counfounds transformation matrix, & preproced dwi
     │   └── anat
     │   └── dwi
 └── sub-02
 ```

Here the goal of this repo is to show **a figure by figure introduction of how to read the html visual quality assessment report**.

The Full illustration is seperated into these parts:
- step0
- step1
- step2

### Step 0, error inspectation
Before you start any further assesment, click on the **Error tab** and see if there is any error reported and it says "No errors to report!"

### Step 1, Anatomical

### Step 2, Denoising

### Step 3, Diffusion
