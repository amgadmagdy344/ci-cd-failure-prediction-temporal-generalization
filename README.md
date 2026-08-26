# ci-cd-failure-prediction-temporal-generalization
Leakage-audited, temporally-evaluated study of explainable CI/CD failure prediction across three repositories
# Beyond Random Splits: Evaluating Temporal Generalization in Explainable CI/CD Failure Prediction

**A Multi-Repository Study**

## Overview

This repository contains the code, data-collection notebook, and final
technical report for an empirical study of CI/CD build failure prediction
across three GitHub repositories (pandas-dev/pandas, scikit-learn/scikit-learn,
facebook/react).

## Key Finding

An initial model appeared to predict CI/CD failures well under random
cross-validation (F1 = 0.65). A feature-level data-leakage audit reduced
this to F1 = 0.481 ± 0.058. Critically, under temporally realistic
evaluation (training on older runs, testing on newer ones), performance
dropped further to F1 ≈ 0.15–0.33, and this gap replicated across all
three repositories tested. A follow-up attempt to close the gap using
past-only historical failure-rate features did not improve temporal
performance in any repository.

**The central finding is methodological**: apparent predictive performance
under random validation can substantially overstate real-world,
future-oriented performance when the underlying process is non-stationary.

## Contents

- `Phase1_Phase2_Final_Report.pdf` — full technical report
- `CI_CD_Failure_Prediction_Analysis.ipynb` — the Colab notebook with all
  code and outputs (data collection, leakage audit, temporal evaluation,
  SHAP analysis)
- `README_notebook.txt` — important note on data reproducibility (the
  GitHub Actions API is live, so re-running the notebook will produce
  slightly different numbers than the frozen report — see this file for
  details)

## Citation

If you use or reference this work, please cite via its Zenodo DOI:

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22078396.svg)](https://doi.org/10.5281/zenodo.22078396)

## Author

Amgad Magdy Ahmed
