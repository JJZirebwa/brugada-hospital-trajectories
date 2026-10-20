# Brugada hospital trajectory analysis

My final-year Biomedical Science research pipeline for retrospective machine-learning stratification of a Brugada-suspect cohort using ICD-10 encoded hospital trajectories.

*Retrospective machine-learning stratification of a Brugada-suspect cohort into SCN5A-mediated genetic architecture classes using ICD-10 encoded hospital trajectories*

The dissertation write-up was awarded **83%**. The work combined cohort construction, hospital-event feature engineering, observability checks and logistic regression, random forest and shallow neural-network comparisons. The main model signal was modest and unstable; record depth, imbalance and limited event support shaped how I interpreted it.

[Read the project and selected results](https://jubileejoyzirebwa.com/case-studies/final-year-project/) · [Dissertation overview](https://jubileejoyzirebwa.com/documents/#dissertation)

## Migration

Migrated on **20 October 2026** from the pipeline previously hosted in my portfolio repository. This standalone repository preserves the final publicly shared code and configuration. The source snapshot is commit `eb5f380af976f8db89c632366199729d7c5a5142`, under `academic/final-year-project/pipeline/`; the 18 code and configuration files were copied without changes. The portfolio repository remains private.

## Follow the analysis

| File | Work it contains |
| --- | --- |
| [`src/build_features.py`](src/build_features.py) | Cohort alignment, hospital-event features, ICD/OPCS groupings and observability controls. |
| [`src/build_features_execute_and_audit.py`](src/build_features_execute_and_audit.py) | Execution wrapper and feature-integrity audit. |
| [`src/feature_engineering_execute_and_audit_driver.py`](src/feature_engineering_execute_and_audit_driver.py) | Staged notebook-style driver. |
| [`src/train_models.py`](src/train_models.py) | Train/test splitting, training-only preprocessing, LR/RF/NN fitting, threshold sweeps, metrics and feature effects. |
| [`src/raw_icd_signalling_pipeline.py`](src/raw_icd_signalling_pipeline.py) | Exploratory raw-code screening and grouped-code modelling. |
| [`src/eda_plots.py`](src/eda_plots.py) | Feature-matrix, missingness and distribution plots. |
| [`src/export_bundle_filter.py`](src/export_bundle_filter.py) | Export review, masking and figure/table preparation. |
| [`config/`](config/) | Feature families, code-group policy, recency, preprocessing, target mappings and investigation controls. |
| [`notebooks/export_bundle_filter_notebook_cells.md`](notebooks/export_bundle_filter_notebook_cells.md) | Export-workflow notebook record. |

## Environment and inputs

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python src/build_features.py --help
python src/train_models.py --help
```

The pipeline expects an authorised cohort table with `participant_id`, index timing and target labels, plus admitted-care, outpatient and emergency-care event tables. The research inputs remain in their governed environment; running the analysis requires separately supplied compatible data.

For feature construction, supply `--cohort-csv`, `--hes-apc-csv`, `--hes-op-csv`, `--hes-ae-csv` and `--out-dir`. For model review, start with the feature and target profiles in `config/`, then select `--model-type lr`, `rf` or `nn`. Preprocessing is fitted on training data after the split.

The accompanying requirements describe the shared Python libraries. This migrated snapshot has been checked for Python syntax and valid configuration; reproducing the research results requires the original governed inputs and research environment.
