<div align="center">

# 🧠 nnUNet-Low-Field-MRI-Segmentation

*Pediatric Hippocampus Segmentation from Low-Field MRI using nnU-Net*

![last commit](https://img.shields.io/github/last-commit/Muhammad-Ahmed-Rayyan/nnUNet-Low-Field-MRI-Segmentation)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![language count](https://img.shields.io/github/languages/count/Muhammad-Ahmed-Rayyan/nnUNet-Low-Field-MRI-Segmentation)

<br>

Built with the tools and technologies:

![Python](https://img.shields.io/badge/Python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![nnU-Net](https://img.shields.io/badge/nnU--Net-blueviolet?style=for-the-badge&logo=openverse&logoColor=white)
![NIfTI](https://img.shields.io/badge/NIfTI%20MRI%20Images-8ac926?style=for-the-badge)
![Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)

</div>

## Overview

This project focuses on **hippocampus segmentation** from **low-field pediatric brain MRI scans**, using [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) — a self-configuring deep learning framework for medical image segmentation. The dataset used comes from the **MICCAI LISA 2024 Challenge** proceedings.


Recommended(If using Google Colab):   
Mount **Google Drive** and store the input files there using the folder structure required by **nnU-Net**.  
This is especially useful in **Google Colab**, where GPU sessions may disconnect or crash — keeping your data on Drive ensures you don't lose progress.

---

## 📂 Dataset Folder Structure

```plaintext
.
├── nnUNet/
    ├── nnUNet_raw/
    │   └── Dataset300_LISA/
    │       ├── imagesTr/           # Input MRI volumes (NIfTI format)
    │       ├── labelsTr/           # Corresponding segmentation masks
    │       └── dataset.json        # Dataset metadata
    ├── nnUNet_preprocessed/        # Preprocessing checkpoints & data
    └── nnUNet_results/             # Model outputs, checkpoints
```

---

## 🧾 Dataset Details

- Name: LISA
- Description: Low-field hippocampus segmentation
- Source/Reference: MICCAI LISA 2024
- Modality: MRI
- Classes:
  - 0 → background
  - 1 → hippocampus

All files are in .nii.gz (NIfTI) format.
- Image: LISA_XXXX_0000.nii.gz
- Label: LISA_XXXX.nii.gz

---

## ⚙️ Preprocessing

Before training, the dataset was:
- Renamed under ID 300 in nnUNet_raw/
- All label pixels with 2.0 were remapped to 1.0 (hippocampus only)
- Preprocessed using:
```
nnUNetv2_plan_and_preprocess -d 300 -c 2d
```

Output generated in nnUNet_preprocessed
Cross-validation split saved in splits_final.json

---

## 🧠 Training

To train the model on Fold 0 using 2D configuration:
```
nnUNetv2_train 300 2d 0
```
- Dataset ID: 300
- Configuration: 2d
- Fold: 0
- Trainer: nnUNetTrainer (default)

---

## 📊 Validation Samples

11 validation cases (based on splits_final.json) were manually copied for inference:
```
LISA_0009, LISA_0020, LISA_0040, LISA_0046,
LISA_0050, LISA_0055, LISA_0061, LISA_0063,
LISA_1003, LISA_1008, LISA_1009
```
---

## 📁 Prediction Output

After running inference, the output folder will contain:

- `.nii.gz` segmentation maps for each test image
- `dataset.json`, `plans.json`, and `predict_from_raw_data_args.json`  
  (used for logging, reproducibility, and metadata)

---

## 🔑 Flags Explained

| Flag | Description |
|------|-------------|
| `-i` | Input folder (usually `imagesTs`) |
| `-o` | Output folder for predictions |
| `-d` | Dataset ID (`300` for `Dataset300_LISA`) |
| `-c` | Configuration (e.g., `2d`, `3d_fullres`) |
| `-tr` | Trainer class used (`nnUNetTrainer` by default) |
| `-f` | Fold number used during training (e.g., `0`) |

---

## 🔗 Useful Resources

- 📘 [nnU-Net Official GitHub](https://github.com/MIC-DKFZ/nnUNet)
- 📖 [Comprehensive Guide to Using nnU-Net](https://towardsai.net/p/l/how-i-use-nnunet-for-medical-image-segmentation-a-comprehensive-guide)

---

## 📜 Acknowledgements

- The **MICCAI LISA 2024 Team** for releasing this important pediatric dataset  
- The developers of [**nnU-Net**](https://arxiv.org/abs/1809.10486) for their impactful open-source work  
- [**Towards AI**](https://towardsai.net/p/l/how-i-use-nnunet-for-medical-image-segmentation-a-comprehensive-guide) for a beginner-friendly walkthrough

---

<div align="center">

⭐ Don’t forget to star this repo on GitHub if you found it helpful!

</div>
