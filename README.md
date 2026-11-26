# SHAP-PAM50-BRCA

Analysis code for the article:

> **SHAP-Guided Selection of Gene Panel with Repeated Nested Cross-Validation and PAM50-Exclusion Benchmarking for Interpretable Breast Cancer Subtype Classification from RNA-Seq, with External Validation on METABRIC**
> Neetu Ahlawat and Vishal Verma, Department of Computer Science & Applications, Chaudhary Ranbir Singh University, Jind, Haryana, India.
> Submitted to *Molecular Genetics and Genomics* (2026).

Corresponding author: Vishal Verma (vishal.verma@crsu.ac.in)

## Overview
SHAP (TreeSHAP) values from a gradient-boosted ensemble are used to select a 300-gene panel for four-class PAM50 subtyping (Basal-like, HER2-enriched, Luminal A, Luminal B) of 514 TCGA-BRCA tumours. The panel and four classifiers (XGBoost, Random Forest, SVM, logistic regression) are evaluated with repeated nested cross-validation and then locked and validated externally on 1,608 METABRIC tumours.

## Repository contents
| File | Purpose | Paper |
|---|---|---|
| `00_TCGA_BRCA_pipeline.ipynb` | Held-out test, repeated nested CV, PAM50 exclusion, stability, SHAP interpretation | Sections 3.1–3.6, 4.1–4.6; Tables 3–11; Figs. 2–8 |
| `01_METABRIC_external_validation.ipynb` | Locked-panel external validation on 1,608 METABRIC tumours | Sections 3.7, 4.7; Tables 12–13; Figs. 9–10 |
| `02_additional_METABRIC_analyses.ipynb` | Comparator panels, original training panel, rank normalisation, class weighting | Sections 4.7–4.8 |
| `03_survival_enrichment_sensitivity.ipynb` | Survival, pathway enrichment, panel-size sweep, hyperparameter tuning | Sections 4.8–4.9; Figs. 11–12 |
| `Fig9_…png` – `Fig12_…png` | Figures 9–12 as reported in the article | |
| `requirements.txt`, `CITATION.cff`, `LICENSE` | Packages, citation information, MIT licence | |

## Data
All data are public and are **not** included in this repository.

| Dataset | File(s) | Source |
|---|---|---|
| TCGA-BRCA gene expression, log2(RSEM+1) | `HiSeqV2` | UCSC Xena, https://xenabrowser.net |
| TCGA-BRCA clinical matrix (PAM50 labels) | `TCGA.BRCA.sampleMap_BRCA_clinicalMatrix` | UCSC Xena |
| METABRIC expression and clinical data | `brca_metabric.tar.gz` | cBioPortal, https://www.cbioportal.org/study/summary?id=brca_metabric |

## How to run (Google Colab)
Run Notebook 0 first for the main TCGA-BRCA results; Notebooks 1–3 are independent of it.

1. Open a notebook in Google Colab (File → Upload notebook, or open it from GitHub).
2. Upload the data files listed above to `/content/`.
3. For Notebooks 0 and 3, choose *Runtime → Change runtime type → T4 GPU* (CPU also works, more slowly).
4. Run the cells from top to bottom. Tables (CSV/XLSX) and figures (PNG) are written to the output folder set in each notebook's Config cell.

Approximate run times: Notebook 0, about 95 min (T4 GPU; set `N_REPEATS = 1` for a 20-min test); Notebook 1, 10–20 min (CPU); Notebook 2, about 1 h (CPU); Notebook 3, about 30 min (GPU) or 2 h (CPU).

## Requirements
Python 3 with the packages in `requirements.txt` (all are available in Google Colab; `gseapy` is installed by Notebook 3 if missing):
```
pip install -r requirements.txt
```
Random seeds: 42 for the held-out split and selection; 42–46 for the five nested repeats.

## Citation
If you use this code, please cite the article (details will be updated after publication). See `CITATION.cff`.

## License
MIT License. See `LICENSE`.
