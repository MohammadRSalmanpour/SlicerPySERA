# 🧩 SlicerPySERA — PySERA Radiomics Extension for 3D Slicer

[![3D Slicer Extension](https://img.shields.io/badge/3D%20Slicer-Extension-blue)](https://github.com/topics/3d-slicer-extension)
[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-stable-green.svg)](#version-history)

**SlicerPySERA** integrates the [**PySERA**](https://github.com/MohammadRSalmanpour/PySERA) radiomics engine into **3D Slicer** as an interactive extension.  
It enables reproducible, IBSI-compliant handcrafted radiomics as well as deep feature extraction directly within the Slicer environment.

---

## 📘 Table of Contents
1. [Overview](#overview)  
2. [Repository Structure](#repository-structure)  
3. [Key Features](#key-features)  
4. [Installation](#installation)  
5. [Usage in 3D Slicer](#usage-in-3d-slicer)  
6. [Data & Batch Expectations](#data--batch-expectations)  
7. [Parameters](#parameters-selected)  
   - [Common (both modes)](#common-both-modes)  
   - [Handcrafted only (IBSI-related)](#handcrafted-only-ibsi-related)  
   - [Deep Feature Mode](#deep-feature-mode)  
8. [Output](#output)  
9. [Troubleshooting](#troubleshooting)  
10. [Integration Notes](#integration-notes)  
11. [Version History](#version-history)  
12. [Contact](#contact)  
13. [Maintenance](#maintenance)  
14. [Authors](#authors)  
15. [Citation](#citation)  
16. [License](#license)  
17. [Support](#support)  
18. [Acknowledgment](#acknowledgment)

---

## 🧠 Overview

SlicerPySERA provides a graphical interface for configuring and running radiomics pipelines on medical images and segmentations within **3D Slicer**. It exposes all relevant IBSI (Image Biomarker Standardisation Initiative)-aligned preprocessing and feature extraction settings directly through the GUI.

It leverages the [PySERA library](https://github.com/MohammadRSalmanpour/PySERA) for computation, ensuring standardized, reproducible, and validated radiomics results.

**Key capabilities:**
- IBSI-compliant handcrafted radiomics and deep features  
- Multi-format compatibility (NIfTI, DICOM, NRRD, RTSTRUCT, etc.)  
- Batch and parallel processing support  
- Comprehensive logs and parameter export for reproducibility  

---

## 📁 Repository Structure

```
pysera/        # Core Python radiomics library used by the extension
PySera/        # ScriptedLoadableModule for 3D Slicer (this extension)
PySeraCLI/     # Optional command-line interface wrapper
PySeraQt/      # Optional Qt-based alternative UI
Data/          # Sample/test data (optional)
```

---

## ⚙️ Key Features

- **Fully integrated with 3D Slicer** – no external scripts required  
- **IBSI-compliant handcrafted features** (morphological, texture, statistical, etc.)  
- **Deep-learning feature extraction** with pretrained models (ResNet50, VGG16, DenseNet121)  
- **Advanced configurability** – bin size, discretization, resampling, intensity rounding  
- **High reproducibility** – parameter snapshot and structured report export  

---

## 💻 Installation

### Option 1 — Scripted Module (recommended)

1. Clone or download this repository.  
2. In 3D Slicer, navigate to:  
   **Edit → Application Settings → Modules → Additional Module Paths**  
   Add the path to the `PySera/` directory, then restart Slicer.  
3. Ensure `pysera` is available to Slicer’s Python:  
   - Simplest: copy `pysera/` into `PySera/lib/pysera/`  
   - Alternatively: install `pysera` into Slicer’s Python interpreter.  
4. After restarting, **PySERA** appears under the *Radiomics* module category.

> 💡 **Note:** The [PySERA library](https://github.com/MohammadRSalmanpour/PySERA) can also be used independently in Python.

---

## 🖥️ Usage in 3D Slicer

1. Load an image and segmentation (mask) into Slicer.  
2. Open **Modules → Radiomics → PySERA**.  
3. Select image and mask inputs, and specify output directories.  
4. Choose **Handcrafted** or **Deep** feature extraction mode.  
5. Adjust **IBSI parameters** (for handcrafted mode).  
6. Select categories/dimensions for feature subsets.  
7. Click **Apply** to start feature extraction.

---

## 📦 Data & Batch Expectations

- Compatible with **NIfTI**, **NRRD**, **DICOM**, and **RTSTRUCT** inputs.  
- Ensure image/mask folder structures are **mirrored** and contain no extra nesting.  
- RTSTRUCT processing uses a temporary cache folder (`temporary_files_path`).  

---

## ⚙️ Parameters (selected)

### 🧭 Common (both modes)

| Parameter | Description |
|------------|-------------|
| `num_workers` | Number of CPU cores or “auto” for automatic selection |
| `enable_parallelism` | Enables multiprocessing if supported |
| `apply_preprocessing` | Apply IBSI-aligned ROI preprocessing |
| `min_roi_volume` | Minimum ROI volume threshold (mm³) |
| `roi_selection_mode` | “per_Img” or “per_region” for ROI grouping |
| `roi_num` | Number of ROIs to process |
| `aggregation_lesion` | Enable multi-lesion feature aggregation |
| `report` | Logging level: “all”, “info”, “warning”, “error”, “none” |
| `temporary_files_path` | Directory for temporary cache files |

---

### 🧩 Handcrafted only (IBSI-related)

| Category | Parameter | Description |
|-----------|------------|-------------|
| **Data Type** | `radiomics_DataType` | Imaging modality (“CT”, “MR”, “PET”, “OTHER”) |
| **Discretization** | `radiomics_DiscType`, `bin_size` | Quantization type (“FBS”/“FBN”) and bin width |
| **Resampling** | `radiomics_isScale`, `radiomics_VoxInterp`, `radiomics_ROIInterp`, `radiomics_isotVoxSize`, `radiomics_isotVoxSize2D`, `radiomics_isIsot2D` | Voxel scaling, interpolation, isotropic resampling |
| **Intensity Handling** | `radiomics_isGLround`, `radiomics_isReSegRng`, `radiomics_ReSegIntrvl01`, `radiomics_ReSegIntrvl02`, `radiomics_isOutliers`, `radiomics_isQuntzStat`, `radiomics_ROI_PV` | Rounding, re-segmentation range, and partial-volume control |
| **IVH Parameters** | `radiomics_IVH_Type`, `radiomics_IVH_DiscCont`, `radiomics_IVH_binSize` | Controls Intensity-Volume Histogram discretization |
| **Feature Precision** | `feature_value_mode` | “REAL_VALUE” or “APPROXIMATE_VALUE” for NaN handling |

---

### 🤖 Deep Feature Mode

| Parameter | Description |
|------------|-------------|
| `extraction_mode` | Set to `"deep_feature"` to enable deep CNN feature extraction |
| `deep_learning_model` | Deep model backbone (`resnet50`, `vgg16`, `densenet121`) |
| *Note:* | IBSI parameters are ignored when using deep feature extraction mode. |

---

## 📊 Output

- **Excel Report** with:
  - `Radiomics_Features`: All extracted features  
  - `Parameters`: Run configuration  
  - `Report`: Warnings or extraction issues  
- **In-Slicer summary log** after each run.

---

## 🧩 Troubleshooting

| Issue | Resolution |
|--------|-------------|
| No visible effect of report level | Ensure report level is set *before* pressing “Apply”. |
| `'str' object is not callable` error | Occurs due to Qt bindings; fixed internally via safe access. |
| Missing output | Verify mirrored image/mask structure and writable destination folder. |
| DICOM RTSTRUCT memory errors | Confirm `temporary_files_path` is on a writable drive. |

---

## 🧱 Integration Notes

- Implemented as a **ScriptedLoadableModule** using Qt/CTK.  
- Parameters are grouped for **Handcrafted** and **Deep** extraction modes.  
- Synchronization maintained between selected categories and dimensions.

---

## 🕒 Version History

```
v1
└─ v1.0
   └─ v1.0.0 — Initial stable release
```

---

## 📬 Contact

For general inquiries or academic collaboration:

**Dr. Mohammad R. Salmanpour (Team Lead)**  
📧 msalman@bccrc.ca · m.salmanpoor66@gmail.com · m.salmanpour@ubc.ca  

---

## 🔧 Maintenance

**Dr. Mohammad R. Salmanpour** – Lead Developer  
**Sirwan Barichin** – GUI Developer  

---

## 👥 Authors

| Name | Role | Contact |
|------|------|----------|
| **Dr. Mohammad R. Salmanpour** | Team Lead, IBSI Standardization, Core Developer | msalman@bccrc.ca |
| **Sirwan Barichin** | GUI Development, Integration, Debugging | sirwanbarichin@gmail.com |
| **Dr. Mehrdad Oveisi** | Evaluator, Software Engineering Advisor | moveisi@cs.ubc.ca |
| **Dr. Arman Rahmim** | Funding, Evaluation, Medical Imaging Expert | arman.rahmim@ubc.ca |

---

## 📚 Citation

If you use this extension or PySERA in your research, please cite both:

```bibtex
@software{slicerpysera2025,
  title     = {SlicerPySERA: A 3D Slicer Extension for IBSI-Compliant Radiomics via PySERA},
  author    = {SlicerPySERA Team},
  year      = {2025},
  url       = {https://github.com/MohammadRSalmanpour/SlicerPySERA}
}

@software{pysera2025,
  title     = {PySERA: A Simple Python Library for Radiomics Feature Extraction},
  author    = {PySERA Team},
  year      = {2025},
  url       = {https://github.com/MohammadRSalmanpour/PySERA}
}
```

---

## ⚖️ License

Released under the **MIT License**.  
See [LICENSE](LICENSE) for details.

---

## 🧭 Support

- Issues: [GitHub Issues](https://github.com/MohammadRSalmanpour/SlicerPySERA/issues)  
- Documentation: This README and module help  
- Examples: See [PySERA Examples](https://github.com/MohammadRSalmanpour/PySERA/tree/main/examples)

---

## 🏛️ Acknowledgment

Supported by:
- **Quantitative Radiomolecular Imaging and Therapy (Qurit) Lab**, UBC, Canada  
- **BC Cancer Research Institute**, Vancouver, Canada  
- **Virtual Collaboration (VirCollab) Group**, Canada  
- **Technological Virtual Collaboration Corporation (TECVICO Corp.)**, Canada  

Funding provided by the **Natural Sciences and Engineering Research Council of Canada (NSERC)** —  
*Idea to Innovation (I2I) Grant GR034192.*

---

*This repository provides the **SlicerPySERA** extension for 3D Slicer.*  
The [**PySERA core library**](https://github.com/MohammadRSalmanpour/PySERA) is maintained separately for standalone Python usage.
