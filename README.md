# MedGuard-UZ-ADE-XAI

Explainable and fairness-audited machine learning framework for serious adverse drug event (ADE) report prioritization using FAERS pharmacovigilance data.

## Project overview

This repository contains reproducibility materials, model outputs, result tables, figures, and manuscript-supporting files for the MedGuard-UZ ADE-XAI study.

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

## Data source

The modelling workflow uses a cleaned FAERS-derived dataset based on FDA adverse event reporting data.

The main raw dataset is not included in this repository because of file-size limitations.

To reproduce the analysis, place the cleaned dataset locally as:

- fda_adverse_events_2015_2026_CLEAN.csv

The dataset should contain FAERS-derived report-level variables such as:

- report_id
- receive_date
- year
- month
- quarter
- serious
- serious_flags
- is_fatal
- is_hospitalized
- is_life_threat
- is_disabling
- reactions
- primary_reaction
- reaction_outcomes
- patient_recovered
- num_reactions
- suspect_drug
- brand_name
- drug_route
- drug_indication
- manufacturer
- pharm_class
- num_drugs
- drug_count_category
- patient_age_years
- age_group
- patient_sex
- patient_weight_kg
- country
- report_age_days
- serious_ade

## Target definition

The target variable is:

- serious_ade

The serious_ade label is a binary target for serious ADE report prioritization.

It can be derived from seriousness-related indicators such as:

- is_fatal
- is_hospitalized
- is_life_threat
- is_disabling

A report is labelled as serious_ade = 1 if at least one seriousness-related flag is positive.

Otherwise, it is labelled as serious_ade = 0.

## Main modelling approach

The project compares multiple machine-learning models, including:

- Logistic Regression
- XGBoost
- CatBoost

The primary manuscript model is a leakage-reduced XGBoost classifier.

## Leakage-reduced model

The primary leakage-reduced model excludes:

- reaction_outcomes

This is done because reaction_outcomes may contain outcome-proxy information and can increase the risk of data leakage.

## Strict leakage-reduced model

A stricter sensitivity analysis additionally excludes:

- primary_reaction
- reactions

Therefore, the strict leakage-reduced model excludes:

- reaction_outcomes
- primary_reaction
- reactions

This conservative model tests whether the model still performs meaningfully without reaction-derived text fields.

## Main reported results

| Analysis | Main result |
|---|---:|
| Full XGBoost AUROC | 0.865 |
| Full XGBoost AUPRC | 0.841 |
| Leakage-reduced XGBoost AUROC | 0.862 |
| Leakage-reduced XGBoost AUPRC | 0.838 |
| Strict leakage-reduced XGBoost AUROC | 0.852 |
| Strict leakage-reduced XGBoost AUPRC | 0.822 |
| Temporal validation AUROC | 0.826 |
| Temporal test AUROC | 0.800 |
| Preferred alert threshold | 0.30 |
| Alert burden reduction at threshold 0.30 | approximately 36.9% |
| Serious ADE sensitivity retained at threshold 0.30 | approximately 90.8% |

## Threshold and alert-tier interpretation

The project evaluates threshold-based alert triage.

The preferred threshold is 0.30.

At this threshold, the leakage-reduced model reduces active alert burden while retaining approximately 91% of serious ADE cases.

The alert tiers are:

- Critical
- High
- Advisory
- Low-risk audit queue

Low-risk reports are not deleted. They are retained in a non-interruptive audit queue for review.

## Explainability

SHAP analysis is used to explain model predictions.

Important SHAP features include:

- country_US
- age_group_Unknown
- num_drugs
- num_reactions
- report_age_days
- primary_reaction_Death
- patient_age_years

These features should be interpreted as report-level pharmacovigilance associations, not as causal clinical mechanisms.

## Fairness audit

Subgroup fairness analysis is performed across:

- patient_sex
- age_group
- country
- drug_count_category

The analysis identified elevated false-negative rates in some subgroups, including:

- female reports
- unknown-sex reports
- infant reports
- teen reports
- unknown-age reports
- single-drug reports
- low-drug-count reports

These findings support future subgroup-specific calibration and continuous fairness monitoring.

## Calibration and confidence intervals

The analysis includes:

- Brier score
- calibration curve / reliability diagram
- bootstrap 95% confidence intervals

Bootstrap confidence intervals are used to estimate uncertainty around performance metrics such as:

- AUROC
- AUPRC
- Sensitivity
- Specificity
- PPV
- NPV
- F1-score
- Brier score

## Intended use

This repository is intended for:

- pharmacovigilance research
- serious ADE report prioritization research
- reproducibility
- model audit
- explainable AI analysis
- fairness auditing
- manuscript support

## Not intended use

This model is not intended for:

- autonomous clinical decision-making
- autonomous alert suppression
- direct bedside ADE risk prediction
- diagnosis
- treatment recommendation
- clinical deployment without external validation
- clinical deployment without local calibration
- clinical deployment without prospective shadow-mode evaluation

## Important limitations

This project has several important limitations:

1. FAERS is a spontaneous reporting system and is affected by reporting bias.
2. The model does not estimate real hospital ADE incidence.
3. The model does not establish causal relationships.
4. Independent external validation has not yet been performed.
5. Temporal drift was observed.
6. Subgroup disparities were observed.
7. The model is not deployment-ready.
8. Low-risk reports may still contain serious ADE cases and should not be deleted.

## Repository contents

This repository may include:

- README.md
- requirements.txt
- data_dictionary.md
- model_card.md
- CITATION.cff
- LICENSE
- notebook files
- model result tables
- leakage sensitivity tables
- strict leakage sensitivity tables
- temporal validation results
- threshold optimization tables
- alert-tier summaries
- fairness audit tables
- SHAP results
- calibration figures
- manuscript-supporting files

## Installation

Install the required Python packages with:

pip install -r requirements.txt

## Main Python dependencies

The main dependencies are:

- pandas
- numpy
- scikit-learn
- xgboost
- catboost
- shap
- matplotlib
- joblib
- openpyxl
- jupyter
- notebook

## Reproducibility workflow

A typical workflow is:

1. Place the cleaned FAERS dataset in the project folder.
2. Open the Jupyter notebook.
3. Load the dataset.
4. Create or verify the serious_ade target.
5. Train baseline models.
6. Train the leakage-reduced XGBoost model.
7. Run strict leakage sensitivity analysis.
8. Run temporal validation.
9. Run threshold optimization.
10. Run SHAP explainability.
11. Run subgroup fairness audit.
12. Generate result tables and figures.

## Example local dataset path

If working on Windows, the dataset may be placed at:

- C:\Users\user\Desktop\Maqola\fda_adverse_events_2015_2026_CLEAN.csv
- E:\faers_data\fda_adverse_events_2015_2026_CLEAN.csv

Update the DATA_PATH variable in the notebook if the file is stored elsewhere.

## Data availability

The raw cleaned FAERS dataset is not stored in this repository because of file-size limitations.

Users should obtain the FAERS-derived dataset separately and place it locally before running the notebooks.

## Citation

If you use this repository, please cite the related manuscript or use the citation information provided in CITATION.cff.

## License

This repository is released under the MIT License unless otherwise specified.

## Safety statement

MedGuard-UZ ADE-XAI is a research framework for pharmacovigilance report prioritization.

It should not be used as a clinical decision-support system without independent validation, local calibration, prospective shadow-mode testing, clinical governance review, and continuous monitoring.
