# Data Dictionary

| Variable | Description |
|---|---|
| report_id | FAERS report identifier |
| receive_date | Date when the report was received |
| year | Report year |
| serious | Original seriousness field |
| serious_flags | Seriousness descriptors such as hospitalization, death, disability, or none |
| is_fatal | Fatal outcome flag |
| is_hospitalized | Hospitalization flag |
| is_life_threat | Life-threatening flag |
| is_disabling | Disability flag |
| reactions | Reported adverse reaction terms |
| primary_reaction | Primary reaction term |
| reaction_outcomes | Reaction outcome descriptors |
| num_reactions | Number of reaction terms |
| suspect_drug | Suspect drug name |
| brand_name | Drug brand name |
| drug_route | Route of drug administration |
| drug_indication | Reported drug indication |
| manufacturer | Manufacturer or reporting company |
| pharm_class | Pharmacological class |
| num_drugs | Number of drugs listed in the report |
| drug_count_category | Drug-count category |
| patient_age_years | Patient age in years |
| age_group | Derived age group |
| patient_sex | Patient sex |
| patient_weight_kg | Patient weight in kilograms |
| country | Reporting country |
| report_age_days | Time-related report-age variable |
| serious_ade | Binary target variable for serious ADE report prioritization |

## Target definition

The target variable `serious_ade` is derived from seriousness-related indicators:

- is_fatal
- is_hospitalized
- is_life_threat
- is_disabling

A report is labelled as `serious_ade = 1` if at least one seriousness flag is positive. Otherwise, it is labelled as `serious_ade = 0`.

## Leakage-related variables

The following variables may contain outcome-proxy information and should be handled carefully:

- reaction_outcomes
- primary_reaction
- reactions
