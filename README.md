# Location of pallidal and subthalamic stimulation volumes predicts Parkinson's outcomes after DBS

Code and processed data for the manuscript *"Location of pallidal and subthalamic stimulation volumes predicts Parkinson's outcomes after DBS."*

## Citation

If you use code or materials from this repository, please cite our article:

Schoen, D., Khalifa, R., Walters, S., et al. Location of pallidal and subthalamic stimulation volumes predicts Parkinson's outcomes after DBS. *Brain Communications* (under review).

## Contents
- `01_ledd.ipynb`: change in levodopa equivalent daily dose (ΔLEDD) vs VTA overlap (primary outcome).
- `02_motor.ipynb`: MDS-UPDRS III change vs VTA overlap (motor subgroup).
- `03_cognitive.ipynb`: neuropsychological change (RCI+PE or SDS) vs VTA overlap (neuropsychological subgroup).
- `04_aggregate_center.ipynb`: outcome-defined aggregate center analysis and comparison with published STN sweet spots.
- `outcomes_data.xlsx`: de-identified patient-level outcomes, covariates and VTA-ROI overlap.
- `cog_tests.xlsx`: de-identified neuropsychological change scores, one sheet per test.
- `aggregate_center_COMs.csv`: aggregate center coordinates (MNI-152).

## Data
248 patients who underwent STN-DBS (n = 109) or GPi-DBS (n = 139) at UCSF between 2016 and 2024. ΔLEDD at approximately 6 months is available for the full cohort. Motor (STN n = 22, GPi n = 20) and neuropsychological (STN n = 25, GPi n = 23) outcomes at approximately 12 months are available for prospectively assessed subgroups. Patients are identified by study code only and no protected health information is included.

## VTA modeling and overlap

Lead localization and stimulation field modeling were performed in Lead-DBS (v3.2). Preoperative T1-weighted MRI and postoperative CT or MRI were coregistered with ANTs and SPM12 and normalized to MNI-152 space. Patient-specific VTAs were estimated with the SimBio finite element method from stimulation parameters at approximately 6 months and thresholded at an electric field magnitude of 0.2 V/mm. Overlap was calculated as the proportion of each region of interest occupied by the binarized VTA, using STN (motor, associative, limbic), GPi (postparietal, prefrontal, premotor, primary motor, sensorimotor, sensory) and GPe sub-territories from the DISTAL atlas (Minimal variant). Full methods are provided in the associated paper.

Individual-level imaging data (including VTA masks) are not shared due to patient privacy considerations. The aggregate center computation in `04_aggregate_center.ipynb` requires these images and will not run in full without them. Investigators seeking access to imaging data for collaborative purposes may contact the corresponding author, Melanie A. Morrison (melanie.morrison@ucsf.edu).

## Usage
Python 3.10+ with `numpy`, `pandas`, `scipy`, `statsmodels`, `scikit-learn`, `matplotlib`, `seaborn`, `openpyxl`, and `nibabel` (notebook 04 only). Set the data file paths at the top of each notebook and run all cells. Figures and result tables are written to a folder beside each notebook.

## Notes
- The train/test split and K-means clustering in the aggregate center analysis are seeded (`random_state=7`) for reproducibility.
- p-values in the overlap analyses are uncorrected. Motor and neuropsychological analyses are exploratory.

## Licenses

* Copyright 2026 UCSF

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at:
[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

* All code files in this repository are licensed under the Apache License 2.0.
* `outcomes_data.xlsx`, `cog_tests.xlsx` and `aggregate_center_COMs.csv` were acquired at the University of California San Francisco and are licensed under the [Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/).

## Acknowledgments

This work was supported by the National Institute of Neurological Disorders and Stroke (R01NS130066) and the National Institute of Biomedical Imaging and Bioengineering (F99EB037629). This project is part of ongoing research in the Radiology-Morrison-lab-UCSF. Special thanks to all contributors and collaborators involved in this work.
