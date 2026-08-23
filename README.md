# Data-Driven Cardiac Modeling from Body Surface Potentials Using Machine Learning

## Project Status
🚧 **Work in Progress**

This project focuses on reconstructing cardiac electrical activity from body-surface potential measurements using a physics-grounded Electrocardiographic Imaging (ECGI) approach.

The current implementation focuses on dataset extraction, preprocessing, signal alignment, and formulation of the ECGI forward and inverse problems. Transfer-matrix estimation and regularized inverse reconstruction are currently under development.

---

## 1. Project Overview

Electrocardiographic Imaging (ECGI) is a non-invasive technique for estimating electrical activity on the heart surface using electrical measurements recorded from electrodes placed on the torso.

The overall objective of this project is to develop a computational pipeline that maps:

Body Surface Potentials (BSP)
→
Cardiac/Pericardial Surface Potentials (HSP)

The project uses anatomical and electrophysiological data from the EDGAR/KIT dataset.

---

## 2. Dataset

The project uses the EDGAR/KIT dataset containing:

- Human anatomical geometry
- Body Surface Potential Map (BSPM) measurements
- Cardiac/pericardial electrophysiological potential data
- Multiple ventricular pacing sites

The current dataset processing considers **8 ventricular pacing sites**.

> The original dataset is not included in this repository. Users should obtain the dataset from its original source and follow its usage/licensing requirements.

---

## 3. Current Data

After preprocessing and alignment, the current dataset contains:

| Data | Dimensions | Description |
|------|------------|-------------|
| BSPM (X) | 1903 × 163 | 163 torso electrode measurements |
| EP_Pericardial (Y) | 1903 × 502 | 502 pericardial/heart-surface potential points |

The rows of X and Y are aligned so that each row represents corresponding physiological samples.

### Input

**BSPM:**

- 163 torso electrodes
- 1903 aligned samples

### Target

**EP_Pericardial / HSP:**

- 502 cardiac/pericardial mesh points
- 1903 aligned samples

---

## 4. Methodology

The project is being developed as a two-stage ECGI problem.

### Stage 1: Forward Problem

The relationship between cardiac surface potentials and body-surface potentials is represented as:

BSP = A × HSP

where:

- BSP = Body Surface Potentials
- HSP = Heart/Pericardial Surface Potentials
- A = Transfer Matrix

The transfer matrix represents how electrical activity originating from the heart appears at the torso electrodes.

---

### Stage 2: Inverse Problem

The objective is to estimate HSP from measured BSP:

BSP → HSP

The inverse problem is ill-posed because:

- There are 163 torso measurements.
- There are 502 unknown cardiac surface potentials.
- The transfer matrix is therefore non-square.
- The inverse problem can be sensitive to noise and numerical instability.

To obtain a stable solution, Tikhonov regularization is being investigated.

The regularized formulation is:

Ĥ = argmin ||AH - BSP||² + λ||H||²

where:

- Ĥ = reconstructed cardiac potentials
- A = transfer matrix
- BSP = measured body-surface potentials
- λ = regularization parameter

---

## 5. Current Workflow

The current project pipeline is:

EDGAR/KIT Dataset
        ↓
Data Extraction
        ↓
Signal Preprocessing
        ↓
BSPM Extraction
        ↓
Pericardial Potential Extraction
        ↓
Data Alignment
        ↓
X = 1903 × 163
Y = 1903 × 502
        ↓
Transfer Matrix Estimation
        ↓
Rank & Conditioning Analysis
        ↓
Tikhonov Regularization
        ↓
Cardiac Potential Reconstruction
        ↓
Validation
        ↓
3D Cardiac Potential Visualization

---

## 6. Completed Work

The following components have currently been completed:

- [x] Dataset extraction
- [x] Body-surface potential preprocessing
- [x] Pericardial potential extraction
- [x] Data alignment
- [x] Construction of BSPM matrix
- [x] Construction of EP_Pericardial matrix
- [x] 163-electrode BSPM representation
- [x] 502-point pericardial potential representation
- [x] ECGI forward-model formulation

---

## 7. Work in Progress

The following components are currently being implemented:

- [ ] Transfer matrix A estimation
- [ ] Rank analysis of A
- [ ] Singular-value analysis
- [ ] Condition-number analysis
- [ ] Tikhonov regularization
- [ ] Regularization parameter selection
- [ ] Cardiac potential reconstruction
- [ ] Reconstruction error analysis
- [ ] Leave-one-pacing-site-out validation
- [ ] 3D heart-surface visualization
- [ ] Comparison with machine-learning baseline

---

## 8. Validation Strategy

The dataset contains eight ventricular pacing sites.

To evaluate generalization, a leave-one-pacing-site-out strategy is planned.

For each experiment:

7 pacing sites
→ Training/transfer-matrix estimation

1 unseen pacing site
→ Testing

This process will be repeated for all eight pacing sites.

---

## 9. Evaluation Metrics

The reconstructed cardiac potentials will be evaluated using:

### Correlation Coefficient

Measures the similarity between reconstructed and ground-truth cardiac potential patterns.

### Relative Error

Measures the difference between reconstructed and ground-truth potentials.

### Normalized RMSE

Measures reconstruction error relative to the magnitude/range of the target signal.

Results will be reported for individual pacing sites as well as overall averages.

---

## 10. Visualization

The final stage will include visualization of cardiac electrical activity on a 3D heart/pericardial mesh.

The planned visualization will compare:

1. Ground-truth cardiac potentials
2. Reconstructed cardiac potentials
3. Reconstruction error

This will provide both quantitative and qualitative evaluation of the ECGI reconstruction.

---

## 11. Technologies Used

- Python
- NumPy
- Pandas
- SciPy
- Matplotlib
- Jupyter Notebook
- MATLAB
- ECGI / inverse problem modeling
- Linear algebra
- Tikhonov regularization
- 3D cardiac visualization

---
## Team Members

- Keerthan 
- Manish
- Nishanth
- Nisarga s
