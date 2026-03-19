# Ear Recognition System (Cross-Age Scenario)

**Work in Progress**

This project focuses on developing a biometric ear recognition system, with special attention to cross-age scenarios (infants vs adults). The goal is to analyze how age differences impact recognition performance and to build models capable of generalizing across these variations.

---

## Overview

Biometric systems often face challenges when dealing with temporal or age-related variations. This project explores ear recognition as a biometric trait, studying its robustness across significantly different age groups.

The system processes ear images, applies preprocessing techniques, and evaluates recognition performance under cross-age conditions.

---

## Objectives

- Analyze ear image datasets across different age groups
- Implement preprocessing and data augmentation techniques
- Explore feature extraction methods using computer vision
- Train and evaluate recognition models
- Study cross-age generalization challenges

---

## 📂 Dataset

Due to size limitations, the dataset is not included in this repository.

You can download it here:

👉 https://drive.google.com/drive/folders/1hoIFPd3fbIU0iNaCQkj8s85ILn9pwcI_?usp=drive_link

Once downloaded, place the data inside the `data/` directory:

```bash
data/
```

---

## ⚙️ Project Structure

```bash
ear-recognition-cross-age/
│
├── notebooks/
│   ├── 01_data_unification.ipynb
│   ├── 02_experiment_setup.ipynb
│   ├── 03_training_pipeline.ipynb
│   └── 04_results_analysis.ipynb
│
├── data/
│   └── (dataset here)
│
├── results/
├── README.md
├── requirements.txt
```

---

## Tech Stack

- Python
- OpenCV
- NumPy / Pandas
- Scikit-learn / PyTorch
- Jupyter Notebooks

---

## Approach

The project follows an experimental pipeline:

1. Data loading and organization  
2. Image preprocessing and augmentation  
3. Feature extraction  
4. Model training  
5. Evaluation and analysis  

---

## Current Status

- Dataset organization and metadata analysis completed  
- Initial preprocessing pipeline implemented  
- Model training and evaluation in progress  

---

## Setup

Install dependencies:

```bash
pip install -r requirements.txt
```

Run notebooks:

```bash
jupyter notebook
```

---

## Notes

This project is part of a final degree project (TFG) in Data Science and Engineering and is actively under development.

---

## Author

Rafa Suárez  
Data & Software Engineer | AI, Computer Vision, LLMs
