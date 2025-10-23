# SlicerPySERA

[![3D Slicer Extension](https://img.shields.io/badge/3D%20Slicer-Extension-blue)](https://github.com/topics/3d-slicer-extension)

**PySERA** — a comprehensive radiomics extraction library integrated with 3D Slicer as an interactive extension.

---

## Overview

SlicerPySERA provides a bridge between the **PySERA radiomics engine** and the 3D Slicer environment. It enables both GUI-driven and automated batch radiomics feature extraction workflows fully compatible with the **IBSI** (Image Biomarker Standardisation Initiative) guidelines.

This extension supports reproducible radiomics pipelines for clinical research, with modular integration for handcrafted and deep features.

---

## Repository Structure

```
pysera/        # Core Python radiomics library (process_batch API)
PySera/        # ScriptedLoadableModule for 3D Slicer (UI wrapper)
PySeraCLI/     # Minimal CLI module for command-line processing
PySeraQt/      # Optional Qt-based module (alternative UI)
Data/          # Placeholder for local or test data
```

---

## Features

* Fully compatible with 3D Slicer module framework
* Batch feature extraction via Python API or GUI
* IBSI-compliant handcrafted feature computation
* Modular architecture supporting deep features
* Open-source and extensible for research

---

## Installation

### Local installation (Scripted module, no build required)

1. Copy the `PySera` directory to **Slicer’s Additional Module Paths** or place it inside the local Slicer modules folder.
2. Ensure `pysera/` is accessible via the Python path (or inside `PySera/lib/pysera/`).
3. Launch 3D Slicer → The module **PySERA** will appear in the module list.

---

## Usage

### From GUI

Open 3D Slicer → Select **PySERA** from the module selector → Load an image and corresponding mask → Configure feature parameters → Run extraction.

---

## License

Licensed under the **MIT License**. See `LICENSE.txt` for details.

---

## Metadata

* **Extension name:** SlicerPySERA
* **GitHub topic:** `3d-slicer-extension`
* **License:** MIT
* **Homepage:** [https://github.com/MohammadRSalmanpour/SlicerPySERA](https://github.com/MohammadRSalmanpour/SlicerPySERA)
* **Icon:** `https://raw.githubusercontent.com/MohammadRSalmanpour/SlicerPySERA/main/Resources/Icons/SlicerPySERA.png`
* **Maintainer:** Mohammad R. Salmanpour
* **Compatible with:** 3D Slicer 5.6+

---

## Acknowledgments

Developed as part of the **PySERA Project** to advance reproducible radiomics in medical imaging through open, integrative tooling in **3D Slicer**.
