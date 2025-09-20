# Chatter-CNN (HDCNN) for online chatter detection in milling

> Online chatter detection for workpiece milling using a hybrid deep CNN (Inception-Chatter + SR-MI) and an early detection method based on a small-probability hypothesis combined with CUSUM.

**Staged Release**
**Code by 2025-10-30** · **Data by 2025-12-30**
**License**: Code — MIT · Data — CC BY 4.0 (planned)

---

## 1. Overview

This repository contains the implementation of **Chatter-CNN (HDCNN)** for online chatter detection in milling, integrating the **Inception-Chatter** module and **SR-MI (Squeeze-Residual Mutual Information)** module. We also release an **early chatter detection** method based on a **small-probability hypothesis + CUSUM**.

**Key features**

* HDCNN with Inception-Chatter & SR-MI modules
* Early-chatter detection (small-probability + CUSUM)
* Force & vibration signal preprocessing pipeline
* Reproducible training/validation/testing with fixed seeds & splits
* One-click scripts to reproduce tables/figures (when full data is available)

---

## 2. Staged Release Plan

| Phase                 | What                                                                                                                                                                                  | When              | Status  |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | ------- |
| **A. Code-first**     | Full implementation (HDCNN, Inception-Chatter, SR-MI), early-detection (small-prob + CUSUM), preprocessing/eval scripts, fixed seeds & splits, **MWE** + **synthetic/example subset** | **by 2025-10-30** | planned |
| **B. Data on Zenodo** | Dataset with paper-aligned train/val/test splits **or** generation scripts + data dictionary; **Dataset Card**; DOI via Zenodo; license: CC BY 4.0 (unless constrained)               | **by 2025-12-30** | planned |
| **Camera-ready DOI**  | Archive the corresponding GitHub Release on Zenodo to issue a versioned, citable DOI                                                                                                  | at camera-ready   | planned |

> If double-blind policy applies, we will provide anonymized/private access to the editor for verification, then switch to public release after acceptance.

---

## 3. Quick Start (MWE)

The **MWE** runs the end-to-end pipeline on a small **synthetic/example subset** so you can verify the code path before the full dataset is public.

```bash
# 1) Clone
git clone <REPO_URL>
cd <REPO_NAME>

# 2) Create env (conda recommended)
conda create -n chattercnn python=3.10 -y
conda activate chattercnn
pip install -r requirements.txt  # or: pip install -e .

# 3) Run the MWE on synthetic/example data
bash scripts/run_mwe.sh

# 4) Inspect outputs (logs, metrics, sample figs)
ls outputs/mwe/
```

**What the MWE includes**

* Minimal preprocessing for force & vibration channels
* Model init (HDCNN) + forward pass + training loop (few epochs)
* Early-chatter detection demo (small-prob + CUSUM)
* Metric report and sample plots

---

## 4. Full Reproduction (after data release)

Once the dataset/DOI is available, you can reproduce the main tables and figures:

```bash
# Download dataset from Zenodo (TBA DOI)
# Place under data/ or set DATA_ROOT
export DATA_ROOT="$(pwd)/data"

# Reproduce all paper results
bash scripts/reproduce_all.sh --data_root "$DATA_ROOT" --seed_cfg configs/seed_config.yaml \
  --splits_file configs/splits.json --exp_cfg configs/experiments.yaml
```

Outputs (metrics, tables, figures) will be written to `outputs/paper/`.

---

## 5. Data Availability

* **Before 2025-12-30**: We provide a **synthetic/example subset** under `data/examples/` whose **interfaces (channel names, sampling rates, windowing, labels)** are consistent with the full dataset, so replacing it later is plug-and-play.
* **By 2025-12-30**: The dataset (or generation scripts + data dictionary) will be archived on **Zenodo** with a DOI (**TBA**). Intended license: **CC BY 4.0**.
* **Constraints**: If some portions are restricted, we will provide a **controlled-access version**/**reproducible subset** and document differences in the **Dataset Card**.

**Dataset Card (will include)**

* Sensors & channels; sampling rates; synchronization
* Machine/tool/workpiece/material parameters; operating ranges
* Windowing strategy; labels (stable/transitional/chatter)
* Quality control, potential biases, and limitations
* License, ethics & compliance; controlled-access process (if any)

---

## 6. Repository Structure (example)

```
.
├── configs/
│   ├── experiments.yaml
│   ├── seed_config.yaml
│   └── splits.json
├── data/
│   └── examples/              # synthetic/example subset
├── scripts/
│   ├── run_mwe.sh
│   └── reproduce_all.sh
├── src/
│   ├── models/                # HDCNN, Inception-Chatter, SR-MI
│   ├── early_detection/       # small-prob + CUSUM
│   ├── preprocessing/         # force/vibration pipeline
│   └── evaluation/
├── outputs/
│   └── (generated)
├── requirements.txt
├── CITATION.cff
├── LICENSE
└── README.md
```

---

## 7. Environment & Determinism

* Fixed random seeds and split file (`configs/splits.json`)
* Version-pinned dependencies (see `requirements.txt`)
* Deterministic flags when supported by the DL backend

---

## 8. License

* **Code**: MIT
* **Data**: CC BY 4.0 (planned; subject to constraints)

---

## 9. Citation

If you find this repository useful, please cite the paper and the Zenodo DOI for the release matching your experiments.

```bibtex
@misc{chattercnn_2025,
  title        = {Chatter-CNN (HDCNN) for Online Chatter Detection},
  author       = {<Your Name(s)>},
  year         = {2025},
  howpublished = {GitHub},
  note         = {Code release by 2025-10-30; Data release by 2025-12-30; DOI: TBA}
}
```

We will add a versioned DOI upon camera-ready via Zenodo.

---

## 10. Changelog

* **2025-10-30** — Planned code release (MIT). Includes MWE and example subset.
* **2025-12-30** — Planned data release (Zenodo DOI; CC BY 4.0). Adds full reproduction scripts for paper tables/figures.

---

## 11. Contact

* Maintainer: Lu
* Email: ylu059@connect.hkust-gz.edu.cn or 202420714@mail.sdu.edu.cn

Issues and pull requests are welcome after public release.
