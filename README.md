# Predictive Analytics Using Machine Learning for Cost Overrun Prediction in Megaprojects

Code accompanying an MSc dissertation in Construction Project Management with BIM, Loughborough University. Supervised by Professor M. Sohail.

## Research questions

- **RQ1**: Cross-national dataset construction and generalisability of cost overrun drivers.
- **RQ2**: Comparative model performance (Linear Regression vs. XGBoost) under repeated out-of-sample validation, addressing the absence of cross-validation in Andrić et al. (2024).
- **RQ3**: SHAP-based feature attribution mapped against Cantarelli et al.'s (2010) four-part causal taxonomy (technical, economic, psychological, political).

## Repository contents

| File | Description |
|---|---|
| `Modelling_2.ipynb` | RQ2 pipeline: preprocessing, Linear Regression and XGBoost models, repeated k-fold cross-validation, baseline comparison, Wilcoxon signed-rank test. |
| `shap_rq3_colab.py` | RQ3 pipeline: SHAP value computation and feature attribution analysis for both fitted models. |
| `requirements.txt` | Pinned package versions used to produce the reported results. |

## Data

The dataset (`Master_Dataset_Rebased_2025_v6.xlsx`, Model_Ready sheet) is not included in this repository. It combines four sources:

- MoSPI Quarterly Project Implementation Status Report (India)
- Chapman, Scandinavia transport dataset (IJPM, 2025)
- Chapman, English Roads POPE dataset
- FTA New Starts Before-and-After (USA)

The primary analysis sample is N=107 projects at or above $500M (2025 PPP), drawn from 216 model-ready rows. The compiled and rebased workbook is not published here as it was assembled in part from data supplied by the dissertation's academic contact; the underlying public sources above can be obtained directly from their respective agencies. [Confirm with Dr Chapman what, if anything, can be shared before treating this as final wording.]

## Methodology summary

RQ2 uses repeated k-fold cross-validation (10 folds x 20 repeats) with pooled out-of-fold scoring, comparing Linear Regression and XGBoost against an on-budget baseline (`DummyRegressor(strategy="constant", constant=0.0)`). `Country` is excluded from the feature set due to collinearity with `Source`. Model comparison uses a paired Wilcoxon signed-rank test on the pooled out-of-fold errors.

RQ3 applies SHAP to both fitted models to attribute prediction behaviour across features, interpreted with reference to the causal taxonomy above rather than as evidence of causal drivers.

## Reproducing the results

Implemented in Python 3.13.15, with scikit-learn 1.6.1, XGBoost 3.4.1 and SHAP 0.52.0 (see `requirements.txt`). A single random seed governs every partition, so the reported figures are exactly reproducible given the same dataset.

1. Install dependencies: `pip install -r requirements.txt`
2. Obtain the dataset from the sources listed above and reproduce the rebasing steps described in the dissertation's methodology chapter (Section 3).
3. Run `Modelling_2.ipynb` for the RQ2 model comparison.
4. Run `shap_rq3_colab.py` for the RQ3 SHAP attribution.

## Citing this repository

Aswathy, S.D. (2026) *cost-overrun-ml-megaprojects* [Source code]. GitHub. Available at: [repository URL] (Accessed: [date]).
