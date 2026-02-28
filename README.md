# Advanced Multi-Modal Sensor Fusion System for Detecting Falling Humans

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue?style=flat-square)](https://opensource.org/licenses/Apache-2.0)
[![Journal: MDPI Vehicles](https://img.shields.io/badge/Journal-MDPI_Vehicles-blue?style=flat-square)](https://doi.org/10.3390/vehicles7040149)
[![DOI](https://img.shields.io/badge/DOI-10.3390%2Fvehicles7040149-blue?style=flat-square)](https://doi.org/10.3390/vehicles7040149)
[![Affiliation: SUMS](https://img.shields.io/badge/Affiliation-Shiga_University_of_Medical_Science-red?style=flat-square)](https://www.shiga-med.ac.jp/english)
[![ISO 26262](https://img.shields.io/badge/Standard-ISO_26262-red?style=flat-square)](https://www.iso.org/standard/43464.html)
[![ORCID](https://img.shields.io/badge/ORCID-0000--0003--4641--0112-A6CE39?style=flat-square&logo=orcid&logoColor=white)](https://orcid.org/0000-0003-4641-0112)

> **Authors:** Dr. Nick Barua¹ · Prof. Masahito Hitosugi²
> ¹ Department of Legal Medicine, Shiga University of Medical Science, Otsu, Shiga, Japan
> **Published:** *Vehicles*, Vol. 7, No. 4, p. 149 (2025) · **Part 1 of 4** in the [AFODS Research Program](#-related-publications)

---

## 📌 Abstract

Collisions with fallen pedestrians pose a lethal challenge to current Advanced Driver Assistance Systems (ADAS). Standard monocular architectures yield a True Positive Rate (TPR) as low as **21.4% at night** for prone individuals — a critical classification gap.

This repository contains the software framework and quantitative evaluation for the **Advanced Falling Object Detection System (AFODS)**. AFODS architecturally integrates **LWIR Thermal**, **NIR Stereo**, and **Ultrasonic** sensors with a custom AI pipeline to achieve **98.2% TPR** in daytime conditions and **95.6% TPR** at night.

---

## 🛠 System Architecture

AFODS integrates four layers to satisfy the redundancy and explainability requirements of **ASIL C/D**:

- **Spatial Detection:** **YOLOv7-Tiny** optimized for edge-case pedestrian postures (prone/falling) — mAP@0.5: 91.3%
- **Predictive Kinematics:** **RNN + Kalman-filter** state estimation — generates alerts **0.3–0.8s** before ground contact
- **Acoustic Verification:** **MFCC-based classification** distinguishes fall acoustic signatures from road noise
- **Explainability:** **SHAP** values provide a forensic audit trail admissible in post-incident reconstruction
- **Hypothermia Detection Mode:** Thermal variance analysis between subject (36.5–37.5°C) and ambient environment

---

## 🧮 Mathematical Logic: Multi-Modal Fusion

### 1. Weighted Detection Probability

The combined detection probability $P_d$ is adjusted dynamically based on environmental temperature variance:

$$P_d = w_{LWIR} \cdot C_{thermal} + w_{NIR} \cdot C_{visual}$$

where $w$ represents the confidence weight and $C$ represents the classifier's confidence score. In low-visibility or thermal-heavy environments, weights are redistributed to maintain system integrity.

### 2. Fall Velocity Estimation

Using NIR stereo disparity, the system calculates vertical velocity ($V_z$) to distinguish a fall from standard pedestrian motion:

$$V_z = \frac{\Delta d}{\Delta t} \cdot \frac{B \cdot f}{Z^2}$$

where $B$ is the stereo baseline and $f$ is the focal length of the NIR stereo pair.

---

## 📊 Performance Benchmarks

AFODS was validated using Anthropomorphic Test Devices (ATDs) and pneumatic fall rigs across forensic-based fall archetypes:

| Condition | TPR (%) | FPR (%) | mAP@0.5 (%) | Latency (ms) |
| :--- | :---: | :---: | :---: | :---: |
| **Daytime, Clear** | 98.2 | 1.8 | 91.3 | 38 |
| **Night, Dry Road** | 95.6 | 3.1 | 88.7 | 42 |
| **Night, Rain** | 89.4 | 5.2 | 83.1 | 51 |
| *Baseline (Monocular, Night)* | *21.4* | *N/A* | *N/A* | *N/A* |

---

## ⚖️ Functional Safety (ISO 26262)

The detection of fallen pedestrians maps to **ASIL C-D** under ISO 26262:

- **Severity (S3):** Life-threatening or fatal injuries
- **Exposure (E3):** Significant occurrence in urban and night environments
- **Controllability (C0):** Near-zero ability for a driver to avoid the hazard once within the classification gap

---

## 🔗 Related Publications

This repository is **Part 1** of a unified 4-paper road safety research program:

| # | Title | Venue | Role |
| :---: | :--- | :---: | :--- |
| **1** | **Advanced Multi-Modal Sensor Fusion System** *(this repo)* | MDPI Vehicles | Technical foundation & benchmarks |
| 2 | [From Post-Mortem to Prevention: Redefining "Invisible" Pedestrians through ISO 26262 and Multi-Modal AI](https://doi.org/10.2139/ssrn.6305618) | SSRN | Problem framing & ISO 26262 compliance |
| 3 | [Integrated Safety Architectures: Leveraging Multi-Modal AI and ISO 26262 to Protect Vulnerable Road Users](https://ssrn.com/author=nick-barua) | SSRN | System-level VRU architecture |
| 4 | Sudden Incapacitation or Death at the Wheel: Unravelling the Predictors of Catastrophic Multi-Vehicle Collisions | SSRN *(pending)* | Epidemiological evidence for ADAS mandate |

---

## 📂 Related Repositories

- **[From-Post-Mortem-to-Prevention-AFODS](https://github.com/Nick-Barua/From-Post-Mortem-to-Prevention-AFODS)** — ISO 26262-aligned
