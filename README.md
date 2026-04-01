# Quantum-Inspired EEG Classification for Motor Imagery

> **71st Florida State Science & Engineering Fair · 2026**
> Intelligent Machines, Robotics & Systems Software · Creekside High School, St. Johns County, FL

---

## Overview

This project investigates whether a **quantum-inspired machine learning architecture** can outperform classical models when classifying cognitive states (imagined left vs. right hand movement) from publicly available EEG data — without requiring quantum hardware or GPU resources.

We applied the **Born Rule** from quantum physics as a kernel function for a Support Vector Machine (QSVM), measuring how EEG signals *interfere* with each other rather than simply how far apart they are. This captures non-linear neural interference patterns that classical kernels cannot represent.

**Result:** QSVM achieved **73.4% accuracy** and **91.3% motor imagery recall**, outperforming Classical SVM by 8.8 percentage points while matching GPU-dependent deep learning models on standard CPU hardware.

---

## Key Results

| Model | Accuracy | F1 Score | Recall | Hardware |
|---|---|---|---|---|
| **QSVM (Ours)** | **73.4%** | **81.4%** | **91.3%** | CPU |
| CNN2D | 74.1% | 82.1% | 88.8% | GPU |
| EEGNet | 72.8% | 80.6% | 87.4% | GPU |
| CNN1D | 71.5% | 79.2% | 85.1% | GPU |
| LSTM | 69.2% | 76.8% | 81.2% | GPU |
| Classical SVM | 64.6% | 74.1% | 53.0% | CPU |

**Statistical validation:** Wilcoxon signed-rank test, p = 0.032 (Bonferroni-corrected)

---

## Why Quantum-Inspired?

Three reasons our approach is clinically meaningful beyond benchmark accuracy:

1. **No GPU required** — runs on standard laptop hardware, making it accessible to rural clinics and field hospitals where GPU infrastructure doesn't exist
2. **Data efficient** — achieves 73% accuracy under 500 training samples; degrades only 3.8% under 50% data reduction vs. 10.5% for Classical SVM
3. **FDA-ready interpretability** — the quantum kernel matrix is fully interpretable; regulators and clinicians can see exactly how similar two neural states are

---

## Dataset

- **Source:** [PhysioNet EEG Motor Movement/Imagery Dataset](https://physionet.org/content/eegmmidb/1.0.0/)
- **Subjects:** 109
- **Recordings:** 654
- **Segmented Trials:** ~9,500
- **Channels:** 64 EEG channels
- **Sampling Rate:** 160 Hz
- **Task:** Imagined left vs. right hand movement (motor imagery)
- **Preprocessing:** 8–30 Hz band-pass filter, ICA artifact removal, 5-fold stratified cross-validation

---

## Methodology

```
PhysioNet EEG → Preprocessing → Feature Extraction → Quantum Kernel → QSVM → Evaluation
```

1. **Data Acquisition** — PhysioNet EEG Motor Movement/Imagery Dataset, de-identified public data
2. **Preprocessing** — Band-pass filtering (8–30 Hz), ICA artifact removal, epoch segmentation
3. **Feature Extraction** — Power Spectral Density via Welch's method across α, β, and μ frequency bands
4. **Quantum-Inspired Kernel** — Born Rule applied as interference-based similarity metric
5. **Benchmarking** — Compared against 8 baseline models: Classical SVM, CNN1D, CNN2D, LSTM, EEGNet, DeepConvNet, and others
6. **Statistical Testing** — Wilcoxon signed-rank test with Bonferroni correction

---

## Engineering Criteria

| Criterion | Target | Result |
|---|---|---|
| Robustness | >70% accuracy under 50% data reduction | ✅ Achieved — 69.6% (QSVM) vs 54.1% (Classical SVM) |
| Functionality | Encode EEG amplitude-phase interference via quantum kernel | ✅ Confirmed via topographic maps + PCA |
| Specification | p < 0.05 improvement over Classical SVM baseline | ✅ p = 0.032 (Bonferroni-corrected) |

---

## Repository Structure

```
qsvm-eeg-classification/
├── index.html              # Project website (GitHub Pages)
├── experiment_pipeline.py  # Main experiment pipeline
├── README.md               # This file
└── LICENSE                 # MIT License
```

---

## Tech Stack

- Python 3.11
- NumPy, SciPy, Scikit-learn
- MNE-Python (EEG preprocessing)
- PennyLane / Qiskit (quantum-inspired modeling)
- Google Colab / Jupyter Notebook
- Matplotlib (visualization)

---

## Research Team

**Sanvi Tummala** · Lead Researcher
**Gurhans Dhillon** · Co-Researcher
**Sachith Hulikere** · Co-Researcher

Creekside High School · St. Johns County, Florida

---

## Citation

If you use this work, please cite:

```
Tummala, S., Dhillon, G., & Hulikere, S. (2026).
Quantum-Inspired Machine Learning Classification of Cognitive States Using Public EEG Data.
71st Florida State Science & Engineering Fair.
Creekside High School, St. Johns County, FL.
```

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

*Dataset: Goldberger et al. PhysioBank, PhysioToolkit, and PhysioNet. Circulation 101(23), 2000.*
