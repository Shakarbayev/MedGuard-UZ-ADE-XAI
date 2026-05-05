# MedGuard-UZ-ADE-XAI

Explainable and fairness-audited machine learning framework for serious adverse drug event (ADE) report prioritization using FAERS pharmacovigilance data.

## Overview

This repository contains the analysis files, model outputs, tables, figures, and reproducibility materials for the MedGuard-UZ ADE-XAI study.

The study evaluates a FAERS-based serious ADE report prioritization framework using:

- base model comparison
- leakage sensitivity analysis
- strict leakage sensitivity analysis
- temporal validation
- threshold optimization
- alert-tier analysis
- SHAP explainability
- subgroup fairness audit
- calibration analysis
- bootstrap confidence intervals

## Study framing

This project is a FAERS-based pharmacovigilance modelling and model-audit study.

It is not a clinical deployment study, not a clinical trial, and not an autonomous clinical decision-support system.

## Data

The main raw dataset is not included in this repository because of file-size limitations.

To reproduce the analysis, place the cleaned FAERS-derived dataset locally as:

```text
fda_adverse_events_2015_2026_CLEAN.csv
