# JEB1433
Hip Arthroscopy Image Registration
This repo is what was used for the JEB1433 project performing 2D/3D image registration on a hip arthroscopy dataset from Johns Hopkins University

---

## Dataset

The pipeline uses **DeepFluoro** (Grupp et al., IPCAI 2020):
- 6 cadaveric pelvis specimens
- Paired CT volumes + real C-arm fluoroscopy images  
- Ground truth camera poses (from offline registration)
- Dataset auto-downloads on first run via `diffdrrdata` (~165 MB, 4× downsampled)

Full dataset: https://doi.org/10.7281/T1/IFSXNV

---

## The DRR Stack

We use **DiffDRR** (Gopalakrishnan & Golland, 2022) which reformulates Siddon's ray casting
algorithm as vectorized PyTorch tensor operations:

- **GPU-accelerated**: Sub-second renders at 512×512 (vs 27–52 seconds in Freund 2004)
- **Auto-differentiable**: Gradient flows from image similarity → DRR pixels → camera pose
- **Siddon's method**: Exact radiologic path integral (not interpolated like projection fields)

This enables **gradient-based optimization** rather than derivative-free Powell's method.

---
