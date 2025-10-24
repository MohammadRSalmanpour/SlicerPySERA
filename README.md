# SlicerPySERA — PySERA Radiomics Extension for 3D Slicer

[![3D Slicer Extension](https://img.shields.io/badge/3D%20Slicer-Extension-blue)](https://github.com/topics/3d-slicer-extension)
[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-stable-green.svg)](#version-history)

**SlicerPySERA** integrates the [**PySERA**](https://github.com/MohammadRSalmanpour/PySERA) radiomics engine into **3D Slicer** as an interactive extension.  
It enables reproducible, IBSI-compliant handcrafted radiomics as well as deep feature extraction directly within Slicer.

---

## Overview

SlicerPySERA provides a graphical interface for configuring and running radiomics pipelines on images and segmentations loaded in 3D Slicer. Feature sets, dimensions, and IBSI-related preprocessing options are available from the module UI. The extension uses the [PySERA library](https://github.com/MohammadRSalmanpour/PySERA) to execute the extraction and save results automatically.

- Handcrafted radiomics (IBSI-compliant) and deep features (pre-trained models)
- Batch processing and optional multiprocessing
- Clear logging and parameter capture for reproducibility
- Works with Slicer data (NIfTI, NRRD, DICOM, RTSTRUCT, etc.)

---

## Repository Structure

```
pysera/        # Core Python radiomics library used by the extension
PySera/        # ScriptedLoadableModule for 3D Slicer (this extension)
PySeraCLI/     # Optional CLI wrapper
PySeraQt/      # Optional Qt-based alternative UI (not required for Slicer)
Data/          # Sample/test data (optional)
```

---

## Features

- **Slicer-native UI** for selecting inputs, tuning IBSI parameters, and choosing feature categories/dimensions  
- **Handcrafted features**: IBSI-compliant first-order, texture, morphology, diagnostics, moment-invariant  
- **Deep features**: ResNet50, VGG16, DenseNet121 (optional mode)  
- **Reproducibility**: parameter snapshot and report export

---

## Installation

### Install as a Scripted Module (no C++ build)

1. Clone or download this repository.
2. In 3D Slicer, go to **Edit → Application Settings → Modules → Additional Module Paths**, add the path to the `PySera/` directory, and restart Slicer.
3. Ensure the `pysera` library is importable in Slicer’s Python:
   - Easiest: copy or add the `pysera/` folder to `PySera/lib/pysera/` (so it’s bundled with the module), **or**
   - Install `pysera` into Slicer’s Python (advanced users).
4. After restart, the **PySERA** module will appear in the **Radiomics** category.

> Note: This extension is designed to run inside 3D Slicer. The [PySERA library](https://github.com/MohammadRSalmanpour/PySERA) can also be used independently in standard Python environments.

---

## Usage (in 3D Slicer)

1. Load an image and segmentation (mask) into Slicer.  
2. Open **Modules → Radiomics → PySERA**.  
3. In the **I/O** tab, choose:
   - **Image File** (or loaded volume)
   - **Mask File** (or loaded segmentation/labelmap)
   - **Destination** and **Temporary** folders  
4. In **Features Extraction Mode**, choose **Handcrafted** or **Deep** and, if deep, select the model.  
5. In **Settings**, adjust:
   - Common options (workers, minimal ROI volume, logging/report level)
   - IBSI parameters (if **Handcrafted** mode) such as discretization, interpolation, isotropic voxel size, re-segmentation thresholds, etc.  
6. Use **Feature Subset** to select categories/dimensions (for handcrafted mode).  
7. Click **Apply**. The module will run extraction, print a status summary, and save outputs (CSV/Excel) to the destination folder.

---

## Data & Batch Expectations

- Works with common medical formats loaded in Slicer (NIfTI/NRRD/DICOM).  
- For DICOM series and RTSTRUCT, ensure consistent patient subfolders and paired image/mask organization if you process from disk (outside Slicer’s scene).  
- When batch-processing folders, keep images and masks in mirrored structures and avoid extra nesting.

---

## Parameters (selected)

**Common (both modes):**  
- `num_workers` (“auto” or integer), `enable_parallelism`, `apply_preprocessing`, `min_roi_volume`, `roi_selection_mode` (“per_Img” / “per_region”), `roi_num`, `aggregation_lesion`, `report`, `temporary_files_path`

**Handcrafted only (IBSI-related):**  
- `radiomics_DataType` (“CT”, “MR”, “PET”, “OTHER”)  
- `radiomics_DiscType` (“FBS” or “FBN”) and `bin_size`  
- Resampling: `radiomics_isScale`, `radiomics_VoxInterp`, `radiomics_ROIInterp`, `radiomics_isotVoxSize`, `radiomics_isotVoxSize2D`, `radiomics_isIsot2D`  
- Intensity handling: `radiomics_isGLround`, `radiomics_isReSegRng`, `radiomics_ReSegIntrvl01`, `radiomics_ReSegIntrvl02`, `radiomics_isOutliers`, `radiomics_isQuntzStat`, `radiomics_ROI_PV`  
- IVH settings: `radiomics_IVH_Type`, `radiomics_IVH_DiscCont`, `radiomics_IVH_binSize`  
- `feature_value_mode` (“REAL_VALUE”, “APPROXIMATE_VALUE”)

**Deep feature mode:**  
- `extraction_mode="deep_feature"` and `deep_learning_model` (`resnet50`, `vgg16`, `densenet121`)  
- Handcrafted-only parameters are not used when deep mode is active.

---

## Output

- **CSV/Excel** output including:
  - `Radiomics_Features` sheet — IBSI-compliant naming for handcrafted or deep feature vectors  
  - `Parameters` sheet — parameter configuration snapshot  
  - `Report` sheet — warnings/errors per case (if logging enabled)
- In-module log summary during extraction.

---

## Troubleshooting

- If the **Report level** has no visible effect, ensure the setting in **Settings → Report** is applied before clicking **Apply**.  
- If you encounter `TypeError: 'str' object is not callable` for `currentText`, note that Qt bindings in Slicer may expose it as a property instead of a callable.  
- Folder-based batch processing requires mirrored image/mask structures with no nested folders.  
- Verify the `temporary_files_path` is writable (used for DICOM-RT mask streaming).

---

## Integration Notes

- Built as a **ScriptedLoadableModule** using Qt/CTK widgets supported by 3D Slicer.  
- All IBSI parameters are organized into **Common** and **Handcrafted-only** groups.  
- Category/dimension synchronization is maintained dynamically.

---

## Version History

```
v1
└─ v1.0
   └─ v1.0.0
```

---

## Contact

SERA is available free of charge.  
For access, questions, or feedback:

**Dr. Mohammad R. Salmanpour (Team Lead)**  
msalman@bccrc.ca · m.salmanpoor66@gmail.com · m.salmanpour@ubc.ca

---

## Maintenance

For technical support and maintenance inquiries:

**Dr. Mohammad R. Salmanpour (Team Lead)**  
msalman@bccrc.ca · m.salmanpoor66@gmail.com · m.salmanpour@ubc.ca

**Sirwan Barichin**  
sirwanbarichin@gmail.com

---

## Authors

- **Dr. Mohammad R. Salmanpour** – Team Lead, Fund Provider, Evaluator, Medical Imaging Expert, Backend Developer, IBSI Standardization, and Slicer GUI Development  
- **Sirwan Barichin** – IBSI Standardization, Debugging, Activation of PySERA Library, and Slicer GUI Development  
- **Dr. Mehrdad Oveisi** – Evaluator, Software Engineer, and Advisor  
- **Dr. Arman Rahmim** – Fund Provider, Medical Imaging Expert, Evaluator, and Advisor  

---

## Citation

If you use this extension or the PySERA library in your research, please cite both as follows:

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

## License

Released under the **MIT License**.  
See [LICENSE](LICENSE) for details.

---

## Support

- Issues: [GitHub Issues](https://github.com/MohammadRSalmanpour/SlicerPySERA/issues)
- Documentation: This README and in-module help  
- Examples: See `examples/` in the PySERA library repository

---

## Acknowledgment

Supported by:

- Quantitative Radiomolecular Imaging and Therapy (Qurit) Lab, University of British Columbia, Vancouver, Canada  
- BC Cancer Research Institute, Department of Basic and Translational Research, Vancouver, Canada  
- Virtual Collaboration (VirCollab) Group, Vancouver, Canada  
- Technological Virtual Collaboration Corporation (TECVICO Corp.), Vancouver, Canada  

Funding provided by the **Natural Sciences and Engineering Research Council of Canada (NSERC)** – *Idea to Innovation (I2I) Grant GR034192.*

---

*This repository distributes the **SlicerPySERA** 3D Slicer extension.  
The [PySERA core library](https://github.com/MohammadRSalmanpour/PySERA) is maintained as a separate, standalone Python package.*
