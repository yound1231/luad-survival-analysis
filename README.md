# TP53 Mutation and Overall Survival in TCGA-LUAD

## Overview

This project investigates the association between **TP53 mutation status and overall survival (OS)** in patients with **lung adenocarcinoma (LUAD)** using publicly available TCGA data.

The analysis follows a standard survival-analysis workflow used in cancer genomics:

- Kaplan–Meier survival estimation
- Log-rank testing
- Multivariable Cox proportional hazards regression
- Proportional hazards assumption assessment using Schoenfeld residuals

The goal of this project is to examine whether the observed association between TP53 mutation status and survival persists after accounting for clinical characteristics.

---

## Research Questions

### Q1 — Unadjusted survival difference

Is overall survival different between **TP53-mutated** and **TP53-wild-type** LUAD patients?

### Q2 — Adjusted association

After accounting for clinical characteristics, is TP53 mutation status associated with overall survival in a Cox proportional hazards model?

Because the proportional hazards assumption was violated for sex and tumor stage in the initial Cox model, these variables were subsequently handled as **stratification variables**, while age was included as a covariate.

---

## Dataset

- **Cancer type:** Lung adenocarcinoma (LUAD)
- **Data source:** The Cancer Genome Atlas (TCGA)
- **Dataset:** TCGA PanCancer Atlas
- **Access:** cBioPortal
- **Clinical data:** Patient/sample-level clinical and survival information
- **Mutation data:** TP53 mutation status

Raw data files are stored locally and are excluded from version control.

---

## Analysis Cohorts

After matching clinical and TP53 mutation data:

- **507 samples** had both clinical and TP53 mutation information.
- **498 samples** had non-missing overall survival time and were included in the Kaplan–Meier and log-rank analyses.
- **486 samples** had complete data for overall survival, TP53 mutation status, age, sex, and stage and were included in the multivariable Cox analysis.

### TP53 mutation status

For the survival analysis, samples were classified as:

- **TP53-mutated:** 260 patients in the KM cohort
- **TP53-wild-type:** 238 patients in the KM cohort

---

## Methods

### 1. Kaplan–Meier Survival Analysis

Kaplan–Meier estimators were used to estimate overall survival separately for TP53-mutated and TP53-wild-type patients.

Overall survival time was measured in months, and death was treated as the event.

The Kaplan–Meier analysis included 498 patients.

### 2. Log-rank Test

A two-group log-rank test was used to evaluate whether the survival distributions differed between TP53-mutated and TP53-wild-type patients.

**Result:**

- Log-rank statistic = 4.38
- p = 0.036

### 3. Cox Proportional Hazards Regression

A multivariable Cox proportional hazards model was initially fitted including:

- TP53 mutation status
- Age
- Sex
- Tumor stage

The initial model showed evidence of proportional hazards violations for sex and tumor stage.

Therefore, a stratified Cox model was fitted with:

- **TP53 mutation status:** primary covariate
- **Age:** continuous covariate
- **Sex:** stratification variable
- **Tumor stage:** stratification variable

### 4. Proportional Hazards Assumption

The proportional hazards assumption was assessed using Schoenfeld residual-based diagnostics.

The initial Cox model showed evidence of non-proportional hazards for sex and tumor stage.

After stratifying on sex and stage, the proportional hazards assumption was not flagged for the remaining covariates.

---

## Results

### Kaplan–Meier Analysis

The unadjusted Kaplan–Meier analysis showed a difference in overall survival between TP53-mutated and TP53-wild-type patients.

**Log-rank p = 0.036**

This indicates that the observed survival distributions differed at the conventional 0.05 significance threshold.

However, this analysis does not account for potential confounding by clinical characteristics.

### Stratified Cox Model

The final stratified Cox model included 486 patients and 174 observed deaths.

| Variable | Hazard Ratio | 95% CI | p-value |
|---|---:|---:|---:|
| TP53 mutation | 1.42 | 1.04–1.94 | 0.027 |
| Age | 1.01 | 1.00–1.03 | 0.072 |

In the stratified Cox model, TP53 mutation was associated with an estimated **1.42-fold hazard of death** compared with TP53 wild-type status, corresponding to an estimated 42% higher hazard.

The 95% confidence interval was 1.04–1.94.

This represents an observational association rather than evidence that TP53 mutation causally increases mortality.

---

## Interpretation

The unadjusted analysis identified a statistically significant difference in overall survival between TP53-mutated and TP53-wild-type patients.

After accounting for age and stratifying by sex and tumor stage to address proportional hazards violations, the association between TP53 mutation and overall survival remained statistically significant in this cohort.

The difference between the initial and stratified Cox models demonstrates the importance of checking model assumptions rather than relying solely on the first fitted regression model.

These findings should be interpreted as an association within this TCGA-LUAD cohort and should not be interpreted as evidence of a causal effect of TP53 mutation on survival.

---

## Limitations

Several limitations should be considered:

1. **Observational study design**  
   The analysis uses retrospective observational data and therefore cannot establish causality.

2. **Potential residual confounding**  
   The model does not account for all clinical or molecular factors that may influence survival.

3. **Limited clinical covariates**  
   The primary multivariable analysis focused on age, sex, and tumor stage.

4. **Stage grouping**  
   Tumor stage was simplified into early-stage (I–II) and advanced-stage (III–IV) groups for modeling.

5. **Complete-case analysis**  
   Patients with missing values in variables required for the multivariable model were excluded from that analysis.

6. **Single-gene analysis**  
   This project focuses specifically on TP53 rather than systematically testing multiple genes.

7. **No external validation**  
   The findings were evaluated within the TCGA-LUAD cohort and were not independently validated in another cohort.

8. **Multiple-testing considerations**  
   Because this project evaluates a predefined TP53 hypothesis rather than screening many genes, a genome-wide multiple-testing correction was not applied.

---

## Reproducibility

The analysis was implemented in Python using:

- `pandas`
- `numpy`
- `matplotlib`
- `lifelines`
- Jupyter Notebook

The complete analysis workflow is contained in:

```text
notebooks/01_data_exploration.ipynb