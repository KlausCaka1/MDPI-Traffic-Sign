# Reliability-Oriented Evaluation of Deep Traffic Sign Classification Models

This repository contains the complete experimental code for the manuscript:

**Comparative Evaluation of Deep Traffic Sign Classification Models under Visual Degradations and Interpretability Analysis**

The study compares five traffic sign classification models under a common evaluation protocol:

1. BaselineCNN
2. ResNet18
3. MobileNetV2
4. MobileNetV2 with Convolutional Block Attention Module
5. Knowledge-distilled MobileNetV2 using ResNet18 as teacher

The experiments evaluate clean GTSRB classification performance, multi-seed training stability, bootstrap confidence intervals, McNemar paired statistical testing, probabilistic calibration, visual-degradation robustness, external GTSDB generalization, computational efficiency, and Grad-CAM diagnostic analysis.

## Repository structure

```text
MDPI-Traffic-Sign/
├── notebooks/
│   ├── traffic_sign_seed_0042.ipynb
│   ├── traffic_sign_seed_0123.ipynb
│   ├── traffic_sign_seed_0777.ipynb
│   ├── traffic_sign_seed_2024.ipynb
│   └── traffic_sign_seed_3407.ipynb
├── requirements.txt
├── README.md
├── LICENSE
├── CITATION.cff
└── .gitignore
```

## Datasets

This study uses two publicly available traffic sign datasets.

### GTSRB

The German Traffic Sign Recognition Benchmark was used for model training, validation, clean testing, and controlled corruption testing.

Official source:
https://benchmark.ini.rub.de/gtsrb_dataset.html

### GTSDB

The German Traffic Sign Detection Benchmark was used only for external validation. Traffic sign regions were cropped from the annotated detection images and mapped to the compatible GTSRB class labels. No GTSDB images were used for training, validation, calibration, or hyperparameter selection.

Official source:
https://benchmark.ini.rub.de/gtsdb_dataset.html

No new dataset was created in this study.

## Experimental protocol

All five model configurations were trained using the same preprocessing, stratified data split, optimizer, learning rate, batch size, and early-stopping strategy. The main experiments were repeated using five independent random seeds:

```text
42, 123, 777, 2024, 3407
```

The seed-specific notebooks correspond to these independent runs. Seed 42 was used for representative qualitative visualizations, including Grad-CAM panels and diagnostic examples. The main quantitative results in the manuscript are based on five-seed summaries unless stated otherwise.

## Evaluation dimensions

The notebooks generate or compute the following analyses:

* Clean GTSRB classification performance
* Accuracy, macro-precision, macro-recall, macro-F1, and weighted-F1
* Bootstrap confidence intervals
* McNemar paired statistical tests
* Expected calibration error, negative log-likelihood, and Brier score
* Severity-wise robustness under blur, central occlusion, low light, and Gaussian noise
* External validation on cropped GTSDB signs
* Parameter count, model size, training time, inference latency, throughput, and peak memory use
* Grad-CAM visualizations and center-concentration diagnostics

## How to run

1. Clone the repository.

```bash
git clone https://github.com/KlausCaka1/MDPI-Traffic-Sign.git
cd MDPI-Traffic-Sign
```

2. Create a Python environment.

```bash
python -m venv .venv
source .venv/bin/activate
```

For Windows:

```bash
.venv\Scripts\activate
```

3. Install dependencies.

```bash
pip install -r requirements.txt
```

4. Download GTSRB and GTSDB from their official sources and place them in the dataset directory expected by the notebooks.

Suggested local structure:

```text
data/
├── GTSRB/
└── GTSDB/
```

The datasets are not redistributed in this repository because they are publicly available from their official sources.

5. Run the notebooks in the `notebooks/` folder.

Recommended order:

```text
traffic_sign_seed_0042.ipynb
traffic_sign_seed_0123.ipynb
traffic_sign_seed_0777.ipynb
traffic_sign_seed_2024.ipynb
traffic_sign_seed_3407.ipynb
```

## Computational environment

The experiments were conducted using:

```text
Python: [insert version]
PyTorch: [insert version]
torchvision: [insert version]
CUDA: [insert version, if applicable]
GPU: [insert GPU model]
Platform: Kaggle notebook environment / local environment [choose correct one]
```

These details should be updated using the actual execution environment before final manuscript submission.

## Outputs

The notebooks save experimental outputs such as figures, tables, trained checkpoints, and evaluation summaries. Large generated files and model checkpoints are not stored in the repository unless explicitly needed for reproducibility.

Recommended output structure:

```text
outputs/
├── figures/
├── tables/
├── metrics/
├── gradcam/
└── checkpoints/
```

## Reproducibility note

The repository is intended to reproduce the analyses reported in the manuscript. Because GPU hardware, CUDA version, and library versions can affect runtime measurements, computational-efficiency results should be interpreted for the stated software and hardware environment.

## License

This repository is released under the MIT License. See `LICENSE` for details.

## Citation

If you use this repository, please cite the associated manuscript and this GitHub repository. Citation metadata are provided in `CITATION.cff`.
