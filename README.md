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

## 📬Contact
SERA is available **free of charge**.
For access, questions, or feedback:

**Dr. Mohammad R. Salmanpour (Team Lead)**  
📧[msalman@bccrc.ca](mailto:msalman@bccrc.ca) | [m.salmanpoor66@gmail.com](mailto:m.salmanpoor66@gmail.com), [m.salmanpour@ubc.ca](mailto:m.salmanpour@ubc.ca)

---

## 🛠️Maintenance
For technical support and maintenance inquiries, please contact:

**Dr. Mohammad R. Salmanpour (Team Lead)**  
 msalman@bccrc.ca – m.salmanpoor66@gmail.com – m.salmanpour@ubc.ca

## 👥Authors
- **Dr. Mohammad R. Salmanpour (Team Lead, Fund Provider, Evaluator, Medical Imaging Expert, Backend Development, Code Refactoring, Debugging, Library Management, IBSI Standardization, and Activation of the PySERA Library, and GUI Development in 3D Slicer)** – [msalman@bccrc.ca](mailto:msalman@bccrc.ca), [m.salmanpoor66@gmail.com](mailto:m.salmanpoor66@gmail.com), [m.salmanpour@ubc.ca](mailto:m.salmanpour@ubc.ca)
- **Sirwan Barichin (GUI Development in 3D Slicer)** – [sirwanbarichin@gmail.com](mailto:sirwanbarichin@gmail.com)
- **Dr. Mehrdad Oveisi (Evaluator, Software Engineer, and Advisor)** – [moveisi@cs.ubc.ca](mailto:moveisi@cs.ubc.ca)
- **Dr. Arman Rahmim (Fund Provider, Medical Imaging Expert, Evaluator, and Advisor)** – [arman.rahmim@ubc.ca](mailto:arman.rahmim@ubc.ca), [arahmim@bccrc.ca ](mailto:arahmim@bccrc.ca)

## 📚Citation

```bibtex
@software{pysera2025,
  title={pysera: A Simple Python Library for Radiomics Feature Extraction},
  author={pysera Team},
  year={2025},
  url={https://github.com/MohammadRSalmanpour/PySERA}
}
```
## 📜License

This open-source software is released under the **MIT License**, which grants permission to use, modify, and distribute it for any purpose, including research or commercial use, without requiring modified versions to be shared as open source. See the [LICENSE](LICENSE) file for details.

## Support

- **Issues**: [GitHub Issues](https://github.com/MohammadRSalmanpour/PySERA/issues)
- **Documentation**: This README and the included guides
- **Examples**: See `examples/basic_usage.py`

## Acknowledgment

This study was supported by:  

- [🔬 **Qu**antitative **R**adiomolecular **I**maging and **T**herapy (Qurit) Lab, University of British Columbia, Vancouver, BC, Canada](https://www.qurit.ca)  
- [🏥 BC Cancer Research Institute, Department of Basic and Translational Research, Vancouver, BC, Canada](https://www.bccrc.ca/)  
- [💻 **Vir**tual **Collab**oration (VirCollab) Group, Vancouver, BC, Canada](https://www.vircollab.com)  
- [🏭 **Tec**hnological **Vi**rtual **Co**llaboration **Corp**oration (TECVICO Corp.), Vancouver, BC, Canada](https://www.tecvico.com)  
We gratefully acknowledge funding from the💰 Natural Sciences and Engineering Research Council of Canada (**NSERC**) Idea to Innovation [**I2I**] Grant **GR034192**.
---

*PySERA - Simple, powerful radiomics in one function call. 🚀*

