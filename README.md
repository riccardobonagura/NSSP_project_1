# NSSP — Project 1

**Neural Signals and Signal Processing (NX-421)** mini-project: single-subject MRI/fMRI analysis of the Language task (*story* and *math*), including preprocessing, GLM and PCA.

**Repository:** [riccardobonagura/NSSP_project_1](https://github.com/riccardobonagura/NSSP_project_1)

## Contents

| File/folder | Contents |
| --- | --- |
| `GroupAI_code.ipynb` | Complete pipeline, visualizations and interpretation of results |
| `utils.py` | FSL configuration and FSLeyes integration |
| `dataset_description.md` | Dataset description |
| `data/` | Local input data and Yeo atlas, excluded from Git |
| `outputs/` | Generated results, excluded from Git |

The pipeline includes BET, FAST, FLIRT/FNIRT registration, removal of the first 10 volumes, MCFLIRT and smoothing at 6 mm FWHM. Subsequent analyses include block and sub-event GLMs, *story–math* contrasts, Harvard–Oxford/Yeo atlas exploration, and 10-component PCA with correlations against GLM regressors.

## Reproducing the results in the course VM

1. **Use the course VM with its graphical desktop and Jupyter**, keeping the provided Python environment. The notebook uses the `Python [conda env:base]` kernel and automatically loads `fsl/6.0.7.18` and `freesurfer/7.4.1`. Dependencies include NumPy, pandas, Matplotlib, NiBabel, Nilearn, scikit-learn, MNE-BIDS, fslpy, FSLeyes/wx and the VM module manager (`import module as lmod`). `utils.py` contains the FSL path specific to this VM.

2. **Clone the repository** from the VM terminal:

   ```bash
   cd /data/Desktop/myfiles
   git clone https://github.com/riccardobonagura/NSSP_project_1.git
   cd NSSP_project_1
   ```

   Use the same commit when comparing runs; `git rev-parse HEAD` returns its identifier.

3. **Copy the same input data used in the analysis** to the following paths, relative to the repository root:

   ```text
   data/T1/T1w.nii.gz
   data/fMRI/tfMRI_LANGUAGE_LR/tfMRI_LANGUAGE_LR.nii.gz
   data/fMRI/tfMRI_LANGUAGE_LR/tfMRI_LANGUAGE_LR_task_onsets.csv
   data/atlas/Yeo2011_7Networks_MNI152_FreeSurferConformed1mm_LiberalMask.nii
   ```

   There must be exactly one `*T1w.nii.gz` file under `data/`. The CSV must contain `onset`, `duration` and `trial_type`, with entries for blocks, sub-events and cues. The Yeo atlas must be provided locally: the notebook does not download it. Harvard–Oxford and the MNI templates are read from the FSL installation.

4. **Open `GroupAI_code.ipynb` from the repository root**, select the kernel above and check that `Project directory` points to `NSSP_project_1`. Set `REDO = True` in the configuration section to recompute cached steps. Select **Restart Kernel and Run All Cells**, without skipping sections: PCA reuses variables, models and atlases defined earlier. FSLeyes requires the graphical session and the `%gui wx` command already included in the notebook.

5. **Keep the notebook parameters unchanged**: `normcorr` registration, 10 discarded volumes, 6 mm smoothing, a PCA mask defined by intensity `> 500` in the first retained volume, 10 components and `random_state=0`. Event onsets are automatically shifted by `10 × TR`; do not adjust the CSV beforehand.

## Outputs and reproducibility checks

Results are saved under `outputs/structural/`, `outputs/functional/` and `outputs/pca/point_1/`, `point_2/`, `point_3/`. They include NIfTI images, transformation matrices, GLM maps, the PCA model, scores, explained variance, figures and correlation CSV files. Some visualizations and tables remain in the notebook/FSLeyes.

The saved notebook run reports **316 initial volumes → 306 retained**, **TR ≈ 0.72 s**, **266603 voxels in the PCA mask**, and approximately **13.92%, 7.83%, 4.41%** explained variance for PC1–PC3. The elbow criterion selects **3 components**.

