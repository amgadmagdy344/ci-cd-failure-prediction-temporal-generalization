Note on reproducing exact figures from this notebook
======================================================

This notebook contains the actual code used to collect data, run the
leakage audit, and perform the temporal/rolling-window evaluations
described in the accompanying report ("Beyond Random Splits: Evaluating
Temporal Generalization in Explainable CI/CD Failure Prediction — A
Multi-Repository Study").

Because the GitHub Actions REST API is live, repeated data pulls may
return slightly different snapshots (the most recent ~4,000 workflow
runs at query time). As a result, if you re-run this notebook today,
the exact figures produced (dataset size, failure counts, F1 scores,
etc.) will differ slightly from those in the frozen PDF report.

This is not an inconsistency in the analysis — it is the same
data-provenance issue documented explicitly in Section 3 and Section
14.1 of the report (referred to there as Pull A, Pull B, and Pull C).
Minor differences in run counts or scores across different executions
of this notebook, or between this notebook and the report, reflect
snapshot timing rather than errors in the methodology.

The authoritative, citable figures are those reported in the frozen
PDF, which reflect the specific data snapshots collected during the
original analysis. This notebook is provided as supporting evidence
of the methodology actually implemented (data collection, leakage
audit, feature engineering, temporal evaluation, SHAP analysis) —
not as a script guaranteed to reproduce identical numbers on a
different date.

For the full, itemized breakdown of which report sections used which
data pull, see Section 14.1 ("Dataset Limitations") of the report.
