# TP53 Mutation and Overall Survival in TCGA-LUAD

## Overview

This project investigates the association between **TP53 mutation status and overall survival (OS)** in patients with **lung adenocarcinoma (LUAD)** using publicly available TCGA data.

The project focuses on applying a practical survival-analysis workflow to cancer genomics data, from data preprocessing and integration to statistical modeling and model diagnostics.

## Research Questions

### Q1. Survival Difference

Is overall survival different between **TP53-mutated** and **TP53-wild-type** LUAD patients?

### Q2. Adjusted Association

After accounting for clinical characteristics, does the association between **TP53 mutation status and overall survival** remain in a Cox proportional hazards model?

---

## Data

- **Cancer type:** Lung adenocarcinoma (LUAD)
- **Data source:** The Cancer Genome Atlas (TCGA)
- **Dataset:** TCGA PanCancer Atlas
- **Accessed through:** cBioPortal
- **Mutation:** TP53
- **Primary outcome:** Overall survival

Clinical and mutation data were downloaded locally and merged using sample identifiers.

Raw data are excluded from version control.

---

## Analysis Workflow

The analysis followed a stepwise survival-analysis workflow:

1. Data preprocessing
2. Clinical and TP53 mutation data integration
3. Kaplan–Meier survival analysis
4. Log-rank test
5. Cox proportional hazards regression
6. Proportional hazards assumption assessment
7. Stratified Cox modeling
8. Interpretation of results

---

## Methods

### Kaplan–Meier Analysis

Overall survival was compared between TP53-mutated and TP53-wild-type patients using Kaplan–Meier survival curves.

The Kaplan–Meier analysis included **498 patients** with available overall survival time and TP53 mutation status.

### Log-rank Test

A two-group log-rank test was used to compare survival distributions between the two TP53 groups.

**Result:**

- Test statistic: **4.38**
- p-value: **0.036**

### Cox Proportional Hazards Model

A multivariable Cox proportional hazards model was used to examine the association between TP53 mutation status and overall survival while accounting for clinical characteristics.

The initial model included:

- TP53 mutation status
- Age
- Sex
- Tumor stage

The proportional hazards assumption was assessed using Schoenfeld residual-based diagnostics.

Sex and tumor stage showed evidence of non-proportional hazards in the initial model. Therefore, these variables were treated as **stratification variables** in the final Cox model.

The final model included:

- **TP53 mutation:** primary covariate
- **Age:** continuous covariate
- **Sex:** stratification variable
- **Tumor stage:** stratification variable

---

## Results

### Kaplan–Meier Survival

The Kaplan–Meier analysis showed a difference in overall survival between TP53-mutated and TP53-wild-type patients.

**Log-rank p = 0.036**

![Kaplan-Meier survival curve](https://github.com/yound1231/luad-survival-analysis/blob/master/results/tp53_kaplan_meier.png)

### Stratified Cox Model

The final stratified Cox model included:

- **486 patients**
- **174 observed deaths**

| Variable | Hazard Ratio | 95% CI | p-value |
|---|---:|---:|---:|
| TP53 mutation | 1.42 | 1.04–1.94 | 0.027 |
| Age | 1.01 | 1.00–1.03 | 0.072 |

The estimated hazard ratio for TP53 mutation was **1.42**.

In this model, TP53-mutated patients had an estimated **1.42-fold hazard of death** compared with TP53-wild-type patients.

The 95% confidence interval was **1.04–1.94**.

This result represents an **observational association** and should not be interpreted as evidence that TP53 mutation causally increases mortality.

---

## Proportional Hazards Assumption

The proportional hazards assumption was assessed using Schoenfeld residual-based diagnostics.

The initial Cox model indicated evidence of non-proportional hazards for:

- Sex
- Tumor stage

These variables were therefore treated as stratification variables in the final model.

After stratification, the remaining covariates did not show evidence of proportional hazards violations in the final model.

---

## Limitations

Several limitations should be considered when interpreting these results:

- This is an **observational analysis**, so causal relationships cannot be established.
- The analysis is based on a **single TCGA-LUAD cohort** and was not externally validated.
- Patients with missing values required for the multivariable analysis were excluded using complete-case analysis.
- Tumor stage was simplified into **I–II vs III–IV** for modeling.
- The model included a limited set of clinical variables and may not account for all potential confounders.
- Only **TP53** was examined in this project; this was not a genome-wide mutation-survival screening analysis.
- The analysis does not account for all possible molecular or treatment-related factors that may influence survival.

---

## Reproducibility

The analysis was performed in Python using:

- `pandas`
- `numpy`
- `matplotlib`
- `lifelines`
- Jupyter Notebook

The main analysis notebook is:

`notebooks/01_data_exploration.ipynb`

The repository contains the analysis code and generated figures, while raw TCGA-derived data are excluded from version control.

---

## Project Structure

- `data/` — raw and processed data
- `notebooks/` — analysis notebooks
- `results/` — generated figures
- `src/` — source code
- `README.md` — project documentation
- `requirements.txt` — Python dependencies

---

## Key Takeaway

This project demonstrates a practical survival-analysis workflow using cancer genomics data:

**data integration → Kaplan–Meier estimation → log-rank testing → Cox regression → assumption checking → stratified modeling → interpretation**

The project also highlights the importance of checking model assumptions rather than relying solely on the results of an initial statistical model.