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
- step 0, error inspectation
- step 1, Anatomical Processing
- step 2, Denosing
- step 3, Diffusion Processing

### Step 0, error inspectation
Before you start any further assesment, click on the **Error tab** and see if there is any error reported and it says "No errors to report!"

### Step 1, Anatomical
#### Brain mask and tissue segmentation of the T1w
![brain mask and tissue segmentation](./figures/sub-01_seg_brainmask.svg)

QSIprep uses anatomical images (T1w or T2w) for robust brain extraction with SynthStrip from FreeSurfer. The boundaries between tissues are highlighted so it can be verified that the segmentation is precise and no gross errors. 

- **Brain mask**: make sure the _red line_ is going around the brain and does not stray into the dura or cut off pieces of the brain, and voxels outside the brain were successfully excluded from the brain mask. 
- **Segmentation**: make sure the _blue line_ follows the boundary between the white matter and the gray matter and isn't cutting off pieces of the white matter

### Step 2, Denoising

### Step 3, Diffusion
