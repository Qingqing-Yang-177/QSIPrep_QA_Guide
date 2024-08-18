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

Note that the visual report elements included are just the default options, other optional results are pending. pls stay in tuned!

The Full illustration is seperated into these parts:
- step 0, error inspectation
- step 1, Anatomical Processing
- step 2, Denosing
- step 3, Diffusion Processing

### Step 0, error inspectation
Before you start any further assesment, click on the **Error tab** and see if there is any error reported and it says "No errors to report!"

### Step 1, Anatomical
#### Brain mask and tissue segmentation of the T1w
![brain_mask_tissue_seg.png](./figures/sub-01_seg_brainmask.svg)

QSIprep uses anatomical images (T1w or T2w) for robust brain extraction with SynthStrip from FreeSurfer. The boundaries between tissues are highlighted so it can be verified that the segmentation is precise and no gross errors. 

- **Brain mask**: make sure the `red line` is going around the brain and does not stray into the dura or cut off pieces of the brain, and voxels outside the brain were successfully excluded from the brain mask. 
- **Segmentation**: make sure the `blue line` follows the boundary between the white matter and the gray matter and isn't cutting off pieces of the white matter

#### T1 to MNI registration
![t1_2_mni.svg](figures/sub-01_t1_2_mni.svg)
<img src="https://github.com/Qingqing-Yang-177/QSIPrep_visual_qa_guide/blob/main/figures/sub-01_t1_2_mni.svg" alt="Animated SVG">


QSIprep also normalizes the anatomical image, whichprovides a registration matrix used to normalize the co-registered dMRI image. 
Ensuring that moving images (registered) match the orientation of fixed images (original T1w), and the anatomical structures are structurally well-aligned. 

### Step 2, Denoising

### Step 3, Diffusion
