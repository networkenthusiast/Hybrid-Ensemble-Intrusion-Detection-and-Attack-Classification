# Hybrid Intrusion Detection and Attack Classification System

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Dataset](https://img.shields.io/badge/Dataset-CICIDS2017-orange)
![Framework](https://img.shields.io/badge/Framework-Hybrid%20Ensemble-success)
![Accuracy](https://img.shields.io/badge/Accuracy-99.79%25-brightgreen)
![ROC-AUC](https://img.shields.io/badge/ROC--AUC-0.9998-green)
![Status](https://img.shields.io/badge/Status-Completed-blue)

---

# Overview

This project presents a **Hybrid Ensemble Intrusion Detection and Attack Classification Framework** that combines supervised learning, unsupervised learning, and ensemble learning techniques for network security analytics.

The framework integrates:

- Binary Random Forest Intrusion Detection
- Kernel PCA + K-Means Clustering
- Multiclass Random Forest Attack Classification
- XGBoost Ensemble Learning

Unlike traditional intrusion detection systems that only determine whether traffic is malicious, the proposed framework also performs **attack attribution**, identifying the likely attack family associated with malicious traffic.

The framework was evaluated using the **CICIDS2017** dataset containing over **2.8 million network flows**.

---

# Key Features

- Binary Intrusion Detection
- Attack-Type Classification
- Unsupervised Traffic Analysis
- Meta-Feature Engineering
- Stacked Ensemble Learning
- Attack Probability Estimation
- Attack Attribution
- Near Real-Time Deployment Capability

---

# System Architecture

```text
CICIDS2017 Dataset
        │
        ▼
Data Preprocessing
        │
        ▼
Feature Selection
        │
 ┌──────┼───────────┐
 │      │           │
 ▼      ▼           ▼

Model 1      Model 2          Model 3
Binary RF    KPCA+KMeans      Attack-Type RF

 │            │                 │
 ▼            ▼                 ▼

rf_pred     cluster_pred    attack_class_pred
rf_prob     cluster_dist_*  attack_prob_*

        └──────┬───────┘
               ▼

      Feature Aggregation

               ▼

        XGBoost Ensemble

               ▼

      Final Intrusion Detection
      + Attack Attribution
```

---

# Dataset

**Source:** CICIDS2017

After attack consolidation:

| Attack Category | Count |
|---------------|-----------:|
| Benign | 2,268,589 |
| DoS_DDoS | 379,554 |
| Reconnaissance | 158,804 |
| Credential_Attack | 15,333 |
| Malware_Compromise | 1,998 |
| Web_Attack | 673 |

**Total Records:** 2,825,951

---

# Model Components

<details>
<summary><b>Model 1 — Binary Random Forest</b></summary>

### Purpose

Detects whether network traffic is:

- Benign
- Attack

### Generated Meta Features

- rf_pred
- rf_prob

### Contribution

Provides supervised attack detection intelligence.

</details>

---

<details>
<summary><b>Model 2 — Kernel PCA + K-Means</b></summary>

### Purpose

Discovers hidden traffic patterns through unsupervised learning.

### Generated Meta Features

- cluster_pred
- cluster_dist_0
- cluster_dist_1

### Contribution

Provides structural and behavioral traffic intelligence.

</details>

---

<details>
<summary><b>Model 3 — Attack-Type Random Forest</b></summary>

### Purpose

Performs multiclass attack categorization.

### Categories

- Benign
- DoS_DDoS
- Reconnaissance
- Credential_Attack
- Malware_Compromise
- Web_Attack

### Generated Meta Features

- attack_class_pred
- attack_prob_Benign
- attack_prob_Credential_Attack
- attack_prob_DoS_DDoS
- attack_prob_Malware_Compromise
- attack_prob_Reconnaissance
- attack_prob_Web_Attack

### Contribution

Provides attack-family intelligence.

</details>

---

# Final Ensemble Model

The final XGBoost classifier combines:

- Original Network Features
- Binary Random Forest Outputs
- Attack-Type Probabilities
- Kernel PCA + K-Means Outputs

This stacked ensemble architecture integrates:

- Behavioral Information
- Attack-Type Information
- Structural Information
- Raw Traffic Characteristics

into a unified prediction framework.

---

# Performance Summary

## Binary Random Forest

| Metric | Value |
|----------|--------:|
| Accuracy | ~99% |
| ROC-AUC | ~0.99 |

---

## Kernel PCA + K-Means

| Metric | Value |
|----------|--------:|
| Accuracy | 83% |
| ROC-AUC | 0.6566 |
| Silhouette Score | 0.4893 |

---

## Attack-Type Random Forest

| Metric | Value |
|----------|--------:|
| Accuracy | ~100% |
| Weighted F1 | ~1.00 |

---

## Final Hybrid XGBoost Model

| Metric | Value |
|----------|--------:|
| Accuracy | 99.79% |
| Precision | 1.00 |
| Recall | 0.99 |
| F1 Score | 0.99 |
| ROC-AUC | 0.9998 |

---

# Key Findings

- Hybrid learning significantly outperformed standalone models.
- Attack-type probabilities were among the most important predictors.
- Clustering-derived features contributed meaningful structural information.
- The ensemble achieved extremely low false positive and false negative rates.
- Learning curves demonstrated strong generalization and minimal overfitting.

---

# Repository Structure

```text
Hybrid-Intrusion-Detection-System/

├── Docs/
|    └──Final-Project-Report-Team-2.pdf
|
├── Presentation/
│   └── Final-Project-Presentation-Team-2.mp4
|   └── Final-Project-Presentation-Team-2.mp4
│
├── Final-Project-Notebook-Team-2.html
|
├── Final-Project-Notebook-Team-2.ipynb
|
├── requirements.txt
├── README.md
└── .gitignore
```

---

# Installation

Clone the repository:

```bash
git clone https://github.com/<username>/<repository>.git
cd <repository>
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Running the Project

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
IDS_multiclass_KPCA.ipynb
```

and execute all cells.

---

# Deployment Strategy

The framework can be deployed as a real-time intrusion detection service using:

- FastAPI
- Flask
- Docker
- AWS
- Azure
- Google Cloud Platform

The architecture supports low-latency inference using CPU-based deployment.

---

# Limitations

- Potential data leakage risks in stacked architectures
- Severe class imbalance for rare attacks
- Limited interpretability
- Validation restricted to CICIDS2017
- Generalization to zero-day attacks requires further study

---

# Future Work

- Leakage-free stacking pipelines
- SHAP and LIME explainability
- Real-time streaming detection
- Deep Learning Models (LSTM, Autoencoders, Transformers)
- Concept Drift Detection
- Cross-Dataset Validation

---

# Authors

### Kalyan Brata Majumder | MS Applied AI | University of San Diego

### Karthik Mekala | MS Applied AI | University of San Diego

### Kunal Gurtoo  | MS Applied AI | University of San Diego

---

# Citation

```text
Majumder, K., Mekala, K., Gurtoo, K.
Hybrid Intrusion Detection and Attack Classification System
University of San Diego
2026
```

---

# Acknowledgements

- CICIDS2017 Dataset
- University of San Diego
- MS in Applied Artificial Intelligence Program
- Scikit-Learn
- XGBoost Community