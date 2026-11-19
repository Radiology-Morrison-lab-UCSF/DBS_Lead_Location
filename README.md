# Location of pallidal and subthalamic stimulation volumes predicts Parkinson's outcomes after DBS

Code and processed data for the manuscript *"Location of pallidal and subthalamic stimulation volumes predicts Parkinson's outcomes after DBS."*

## Citation

If you use code or materials from this repository, please cite our article:

Schoen, D., Khalifa, R., Walters, S., et al. Location of pallidal and subthalamic stimulation volumes predicts Parkinson's outcomes after DBS. *Brain Communications* (in press).

## Contents

Analysis notebooks:
- `01_ledd.ipynb`: change in levodopa equivalent daily dose (ΔLEDD) vs VTA overlap (primary outcome).
- `02_motor.ipynb`: MDS-UPDRS III change vs VTA overlap (motor subgroup).
- `03_cognitive.ipynb`: neuropsychological change (RCI+PE or SDS) vs VTA overlap (neuropsychological subgroup).
- `04_aggregate_center.ipynb`: outcome-defined aggregate center analysis and comparison with published STN sweet spots.

Data (`data/`):
- `outcomes_data.xlsx`: patient-level ΔLEDD, MDS-UPDRS III change scores, covariates (age, sex, target, implant laterality) and VTA-ROI overlap. Used by `01_ledd.ipynb`.
- `motor_outcomes_data.xlsx`: motor subgroup outcomes, covariates and VTA-ROI overlap. Used by `02_motor.ipynb`.
- `cog_tests.xlsx`: neuropsychological scores and change scores, one sheet per test. Used by `03_cognitive.ipynb`.
- `efield_analysis_ready.csv`: per-hemisphere stimulation parameters, VTA volume and electric field metrics (mean and integrated field magnitude, overlap recomputed from the native field grid) for each region. Underlies the sensitivity analyses in Supplementary Tables S8 to S10.

## Data

245 patients who underwent STN-DBS (n = 107) or GPi-DBS (n = 138) at UCSF between 2016 and 2024. ΔLEDD at approximately 6 months is available for 244 patients (STN n = 107, GPi n = 137). Motor (STN n = 22, GPi n = 20) and neuropsychological (STN n = 25, GPi n = 23) outcomes at approximately 12 months are available for prospectively assessed subgroups.

Patients are identified by study code only. Medical record numbers and all dates (birth, surgery) have been removed, and ages are rounded to whole years. Because the analyses used unrounded ages, age-adjusted results rerun from these files may differ slightly from the published values.

## VTA modeling and overlap

Lead localization and stimulation field modeling were performed in Lead-DBS (v3.2). Preoperative T1-weighted MRI and postoperative CT or MRI were coregistered with ANTs and SPM12 and normalized to MNI-152 space. Patient-specific VTAs were estimated with the SimBio finite element method from stimulation parameters at approximately 6 months and thresholded at an electric field magnitude of 0.2 V/mm. Overlap was calculated as the proportion of each region of interest occupied by the binarized VTA, using STN (motor, associative, limbic), GPi (postparietal, prefrontal, premotor, primary motor, sensorimotor, sensory) and GPe sub-territories from the DISTAL atlas (Minimal variant). Full methods are provided in the associated paper.

Individual-level imaging data (including VTA masks) are not shared due to patient privacy considerations. The aggregate center computation in `04_aggregate_center.ipynb` requires these images and will not run in full without them. Investigators seeking access to imaging data for collaborative purposes may contact the corresponding author, Melanie A. Morrison (melanie.morrison@ucsf.edu).

## Usage

Python 3.10+ with `numpy`, `pandas`, `scipy`, `statsmodels`, `scikit-learn`, `matplotlib`, `seaborn`, `openpyxl`, and `nibabel` (notebook 04 only). Set the data file paths at the top of each notebook to the `data/` folder and run all cells. Figures and result tables are written to a folder beside each notebook.

## Notes

- Regression models are adjusted for age, sex and implant laterality (bilateral, left-only or right-only).
- The train/test split and K-means clustering in the aggregate center analysis are seeded (`random_state=7`) for reproducibility.
- p-values in the overlap analyses are uncorrected; Benjamini-Hochberg false discovery rate-adjusted values are reported in the paper. Motor and neuropsychological analyses are exploratory.

## Licenses

* Copyright 2026 UCSF

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at:
[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

* All code files in this repository are licensed under the Apache License 2.0.
* The data files in `data/` were acquired at the University of California San Francisco and are licensed under the [Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/).

## Acknowledgments

This work was supported by the National Institute of Neurological Disorders and Stroke (R01NS130066) and the National Institute of Biomedical Imaging and Bioengineering (F99EB037629). This project is part of ongoing research in the Radiology-Morrison-lab-UCSF. Special thanks to all contributors and collaborators involved in this work.
