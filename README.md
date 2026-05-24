# ESOL Solubility Predictor (RDKit + scikit-learn)

## Overview
This project demonstrates a **physics-informed machine learning workflow** for predicting aqueous solubility (logS) from molecular structure — directly transferable to ADMET property prediction in drug discovery and materials property modeling.

## Results
| Metric | Value | Context |
|--------|-------|---------|
| **R²** | 0.805 | Explains 80% of variance with scaffold-aware splitting |
| **RMSE** | 0.838 | Within benchmark range for RF/Morgan models on ESOL |
| **Top Feature** | LogP (81.5%) | Physically meaningful: hydrophobicity drives solubility |

## Methodology
1. **Featurization**: Morgan fingerprints (2048-bit) + 5 physicochemical descriptors (LogP, MW, TPSA, HBD, HBA)
2. **Splitting**: Scaffold-aware (Murcko scaffolds) to mimic real-world generalization
3. **Model**: Random Forest Regressor (100 estimators)
4. **Validation**: Hold-out test set (119 compounds, ~10% of dataset)

## Key Findings
- **LogP dominates** (81.5% feature importance) — aligns with first-principles understanding of hydrophobicity-driven solubility
- **Scaffold splitting** reduces overoptimism vs. random splitting (R² drops from ~0.87 to ~0.80, but more realistic)
- **5 interpretable descriptors** outperform 2048 fingerprint bits alone

## Reproducibility
```bash
# Create environment
conda env create -f environment.yml
conda activate drugdev

# Run notebook
jupyter notebook notebook.ipynb