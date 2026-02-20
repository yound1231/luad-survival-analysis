# LUAD Survival Analysis (TCGA)

## Project Overview
This project investigates whether **TP53 mutation status** is associated with **overall survival (OS)** in patients with **lung adenocarcinoma (LUAD)** using data from TCGA.

## Research Questions
- **Q1:** Is overall survival different between **TP53-mutated** and **TP53-wildtype** LUAD patients?
- **Q2:** After adjusting for clinical covariates (age, sex, tumor stage), does TP53 mutation remain significant in a **Cox proportional hazards model**?

## Data Source
- TCGA-LUAD (PanCancer Atlas)
- Accessed via cBioPortal
- Clinical data and mutation data downloaded locally

## Methods
- Kaplan–Meier survival analysis
- Log-rank test
- Cox proportional hazards regression model

## Planned Outputs
- Kaplan–Meier survival curve
- Log-rank test p-value
- Hazard ratios (HR) with 95% confidence intervals
- Model interpretation and limitations

## Notes
Raw data files are stored locally and excluded from version control.