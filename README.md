# Beyond Random Splits: Evaluating Temporal Generalization in Explainable CI/CD Failure Prediction

**A Multi-Repository Study**

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22078396.svg)](https://doi.org/10.5281/zenodo.22078396)

> Leakage-audited, temporally-evaluated study of explainable CI/CD failure prediction across three GitHub repositories.

## Overview

This repository contains the analysis notebook, technical report, and reproducibility notes for an empirical study of CI/CD build failure prediction across three GitHub repositories:

- `pandas-dev/pandas`
- `scikit-learn/scikit-learn`
- `facebook/react`

The study investigates whether apparent predictive performance under random evaluation remains valid when models are evaluated on temporally newer workflow runs.

## Research Questions

### RQ1
To what extent can machine-learning models predict CI/CD build outcomes using pre-execution features, and does this performance hold under realistic temporally ordered evaluation?

### RQ2
Which workflow and timing-related factors contribute most strongly to model predictions?

### RQ3
Can SHAP-based explanations provide interpretable insight into the factors driving failure predictions, and what limitations arise when temporal generalization is weak?

## Key Finding

An initial Random Forest model achieved a failure-class F1-score of **0.65** under a random stratified split. A feature-level leakage audit identified an execution-dependent duration feature and a preprocessing leakage issue. After correcting these issues, leakage-free 5-fold cross-validation produced **F1 = 0.481 ± 0.058**.

Under temporally realistic evaluation, performance dropped substantially:

| Repository | Random CV F1 | Temporal F1 |
|------------|---------------|-------------|
| pandas | 0.481 ± 0.058 | 0.198 |
| scikit-learn | 0.516 ± 0.218 | 0.33 |
| react | 0.661 ± 0.114 | 0.26 |

The same direction of degradation was observed across all three repositories.

A follow-up experiment using a strictly past-only historical failure-rate feature did not improve temporal performance under the evaluation protocols used.

### Central Finding

**The central finding is methodological:** apparent predictive performance under random validation can substantially overstate real-world, future-oriented performance when the underlying CI/CD process is non-stationary.

## Methodology

The study follows a leakage-audited and temporally ordered evaluation pipeline:

1. Collect GitHub Actions workflow-run data through the GitHub Actions API.
2. Remove non-executed outcomes such as `skipped` and `cancelled`.
3. Construct pre-execution features from workflow type and execution timestamp.
4. Audit all features for execution-time leakage and preprocessing leakage.
5. Train a class-weighted Random Forest classifier.
6. Evaluate using leakage-free stratified cross-validation.
7. Evaluate temporal generalization using chronological and expanding-window walk-forward evaluation.
8. Replicate the pipeline across multiple repositories.
9. Apply SHAP analysis for model interpretation.
10. Test whether a past-only historical failure-rate feature improves temporal performance.

## Leakage Audit

The initial model included `duration_seconds`, which depends on the workflow's completion time and is therefore unavailable before execution.

The audit also identified preprocessing leakage in workflow-category grouping when category thresholds were computed using the full dataset.

After removing `duration_seconds` and fitting preprocessing only on the appropriate training data, the estimated predictive performance decreased substantially.

## Explainability

SHAP analysis identified workflow type—particularly the `Unit Tests` workflow—as the strongest contributor to model predictions, followed by `hour_of_day` and `day_of_week`.

These explanations should be interpreted as associations learned from the historical dataset, not as causal relationships or guaranteed future predictors.

## Repository Contents

- `technical_report.pdf` — Full technical report containing the study methodology, experiments, results, limitations, and conclusions.
- `CI_CD_Failure_Prediction_Analysis.ipynb` — Colab/Jupyter notebook containing data collection, preprocessing, leakage auditing, temporal evaluation, multi-repository analysis, and SHAP analysis.
- `README_notebook.txt` — Reproducibility note explaining differences that may occur when the notebook is rerun against the live GitHub Actions API.
- `README.md` — Project overview and documentation.

## Reproducibility Note

The analysis uses data retrieved from the live GitHub Actions API. Because workflow-run data changes over time, rerunning the notebook may produce results that differ from the frozen figures reported in the technical report.

For the authoritative reported figures, refer to the frozen technical report. The notebook is provided as supporting evidence of the implemented methodology and analysis.

See `README_notebook.txt` for additional details.

## Limitations

The study has several important limitations:

- The repositories were observed over relatively short time windows.
- Some repositories contain relatively few failure cases.
- The feature set is intentionally limited and does not include richer commit-level or infrastructure-level information.
- The study evaluates a single primary model family (Random Forest).
- The temporal results should not be interpreted as a formal proof of concept drift.
- The study focuses exclusively on GitHub Actions data.

## Citation

If you use or reference this work, please cite the archived Zenodo version:

**DOI:** https://doi.org/10.5281/zenodo.22078396

## Author

**Amgad Magdy Ahmed**
