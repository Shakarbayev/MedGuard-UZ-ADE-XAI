# Model Card: MedGuard-UZ ADE-XAI

## Model type

XGBoost binary classifier.

## Task

Serious adverse drug event report prioritization.

## Target

`serious_ade`

## Primary model

Leakage-reduced XGBoost excluding `reaction_outcomes`.

## Strict sensitivity model

Strict leakage-reduced XGBoost excluding:

- reaction_outcomes
- primary_reaction
- reactions

## Intended use

Research use for pharmacovigilance report prioritization and model audit.

## Not intended use

The model is not intended for autonomous clinical decision-making, autonomous alert suppression, diagnosis, treatment recommendation, or direct patient-level risk prediction.

## Main results

| Model | AUROC | AUPRC |
|---|---:|---:|
| Full XGBoost | 0.865 | 0.841 |
| Leakage-reduced XGBoost | 0.862 | 0.838 |
| Strict leakage-reduced XGBoost | 0.852 | 0.822 |
| Temporal test | 0.800 | 0.788 |

## Key limitations

- FAERS spontaneous-report bias
- no causal inference
- no direct hospital incidence estimation
- no independent external validation
- temporal drift
- subgroup disparities
- not deployment-ready
