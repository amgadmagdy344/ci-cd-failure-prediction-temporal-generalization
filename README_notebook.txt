Note on reproducing exact figures from this notebook
======================================================

This notebook contains the code used to collect data, run the leakage
audit, and perform the temporal/rolling-window evaluations described in
the accompanying report ("Beyond Random Splits: Evaluating Temporal
Generalization in Explainable CI/CD Failure Prediction — A
Multi-Repository Study").

IMPORTANT — pandas-dev/pandas cells specifically:
The pandas-related cells in this notebook were re-run after the report
was finalized. Because the GitHub Actions API returns the most recent
runs at query time, this later run pulled a different snapshot
(2,086 cleaned runs) than the ones the report's frozen figures are
based on (Pull A: 2,037 runs; Pull B: 2,007 runs; Pull C: a further
refresh — see Section 3 and 14.1 of the report). As a result, the
pandas-related numbers currently shown in this notebook's outputs
(e.g. random-CV F1 ≈ 0.59, pooled temporal F1 ≈ 0.48) do not match the
report's authoritative pandas figures (random-CV F1 = 0.481 ± 0.058;
pooled temporal F1 = 0.198). A disclaimer to this effect appears as the
first cell of the notebook itself.

The scikit-learn/scikit-learn and facebook/react cells later in the
notebook were not re-run after the report was finalized and match the
report's figures exactly.

This is the same live-API data-drift issue documented throughout the
report (Sections 3, 6.1, 9, 14.1) — this is simply a further instance
of it, occurring after the report was frozen. It is not an error in
the analysis; it reflects the reality of working with a live,
continuously updated data source.

For the authoritative, citable figures, refer to the frozen PDF report
and its companion Results Log — not to this notebook's current
pandas-related outputs. This notebook is provided as supporting
evidence of the methodology actually implemented (data collection,
leakage audit, feature engineering, temporal evaluation, SHAP
analysis), not as a script guaranteed to reproduce identical numbers
on a different date.
