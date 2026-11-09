# Project 4 - Bank Marketing: contact history and campaign prioritization

**Status: official original data downloaded; the data-understanding notebook has been executed and verified. No packages have been installed and no model has been trained.**

## Project objective

Compare whether a shared model or separate models for clients with and without prior-campaign contact history better predict term-deposit subscription and rank a limited outreach list.

The intended decision point is **before the first call of the current campaign**. The project is a retrospective predictive study of historically contacted clients. It does not establish the effect of making a call or identify customers who benefit because of outreach.

## Dataset and target

- Official source: [UCI Bank Marketing](https://archive.ics.uci.edu/dataset/222/bank+marketing).
- Downloaded variant: the original `bank-full.csv` from `bank.zip`. Verified locally: 45,211 rows and 17 columns, comprising 16 input variables plus `y`.
- Do not substitute the sampled `bank.csv` or the different `bank-additional-full.csv` variant without reviewing the design.
- Outcome: `y`, whether the client subscribed to a term deposit. Encode `yes` as 1 and `no` as 0 after validating the values.
- Preserve the original downloaded archive, documentation, and CSV unchanged in `data/raw/`. Record their source, retrieval date, file sizes, and hashes when downloaded.

## Data saved locally

Downloaded from the official UCI repository on 2026-11-07:

- `data/raw/bank_marketing_uci_original.zip`: untouched UCI download, containing the original and additional variant archives.
- `data/raw/bank.zip`: untouched original-variant archive.
- `data/raw/bank-full.csv`: full original dataset, extracted unchanged.
- `data/raw/bank-names.txt`: official original-variant description and data dictionary, extracted unchanged.
- `reports/source_manifest.json`: source URLs, attribution, retrieval time, file sizes, SHA-256 hashes, and basic validation results.

Read the CSV with a **semicolon delimiter** (`sep=";"` in pandas). Basic checks found 39,922 `no` and 5,289 `yes` values in `y`; the history groups contain 36,954 rows with `previous == 0` and 8,257 with `previous > 0`. No invalid or missing `previous` values or mismatches between `previous == 0` and `pdays == -1` were found. These checks do not replace a full data-quality review.

The bundled dictionary documents date ordering from May 2008 through November 2010. Source row order has been preserved. The CSV lacks full timestamps and customer IDs, so exact chronology and repeat-client separation cannot be independently reconstructed from those identifiers.

The sampled `bank.csv` and different `bank-additional` variant have not been extracted. Use `bank-full.csv` for this project. UCI lists the dataset under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); attribution is retained in the source manifest and original dictionary.

## Contact-history segments

Use `previous`, the number of contacts before this campaign:

- **No prior-campaign contact history:** `previous == 0`.
- **Prior-campaign contact history:** `previous > 0`.

These are contact-history segments, not new versus existing bank customers. Check consistency with `pdays` and `poutcome`; retain the distinction between no prior contact, missing information, and an unknown prior outcome. Do not recode `poutcome="unknown"` as `failure`: an unknown prior outcome is distinct from a recorded failure and from no prior contact. Review invalid or missing `previous` values before assigning segments.

## Three approaches to compare

1. **Pooled common-feature model:** one model for all rows, using the same verified pre-call client features and no contact-history predictors.
2. **Pooled history model:** one model for all rows, adding verified prior-campaign information, including `previous`, `poutcome`, and a history indicator where appropriate. Exclude `pdays` from the primary model.
3. **Separate segment models:** train one model for each contact-history segment. The no-history model uses the common features; the history model may also use verified history features. Combine their predictions for overall evaluation.

Candidate model families are Logistic Regression, Random Forest, and XGBoost. Begin with a simple baseline; algorithm choice and model complexity remain open until the data and validation design are reviewed.

## Prediction timing and leakage checks

The initial common-feature candidates are `age`, `job`, `marital`, `education`, `default`, `balance`, `housing`, and `loan`. Confirm when each was recorded before treating it as available at the decision point.

Exclude the final/current-campaign call fields `day`, `month`, `duration`, `campaign`, and `contact` from the pre-first-call feature set. The recorded last-contact date, duration, accumulated contact count, and contact type do not establish what was available before the campaign's first call.

Exclude `pdays` from the primary models across all three approaches. Its reference date is not established as the start of the current campaign, so do not assume the recorded interval was available before the first call. Any later use belongs in a separately justified sensitivity analysis after timing review. Other history fields also need timing review; keep any unresolved field out of the primary feature set.

The retrospective record may not reconstruct a true pre-first-call snapshot. If timing cannot be established, narrow the claim to a leakage-aware retrospective comparison rather than presenting the model as deployment-ready.

## Evaluation plan

- Preserve source row order. Verify the original full file's documented date ordering before defining a chronological split. Do not reconstruct multi-year chronology by sorting only `month` and `day`.
- Reserve the same later chronological holdout rows for all three approaches. Choose the cutoff after inspecting coverage and segment counts, then freeze it before model selection.
- Split the full dataset first, then divide each split into history segments. Do not give the separate models their own unrelated holdouts.
- Use only earlier data for fitting, preprocessing, tuning, calibration, and threshold selection. Use time-respecting validation within the training period.
- Compare overall and within-segment PR AUC, ROC AUC, calibration, and precision/recall/lift at agreed outreach capacities. Compare ranking approaches on the same total outreach budget.
- Report segment sizes and uncertainty. The smaller history segment may have less stable estimates, and scores from separate models must be comparable before being ranked together.
- Review the unit of analysis and repeat-client risk. Do not assume one row is one unique person; the original file does not provide a customer identifier for a verified customer-disjoint split.

The observed population was selected for historical contact, so performance may not transfer to all bank clients. Subscription prediction is not causal uplift, incremental conversion, or proof that contacting the highest-scoring clients improves results.

## Possible wrap-up: contact-count analysis

After the primary model comparison, optionally summarize observed subscription rates by current-campaign contact count (`campaign`), with group sizes. Keep this descriptive and separate from the pre-first-call models: contact counts reflect the campaign process and stopping decisions, so this analysis cannot establish the effect of an extra call or an optimal number of calls. `campaign` remains excluded from the primary models.

## Folder map

```text
04_bank_marketing_history_segmentation/
|-- data/
|   |-- raw/          # Untouched source archive, documentation, and CSV
|   `-- processed/    # Later validated transformations
|-- notebooks/       # Small analysis steps reviewed together
|-- reports/         # Data review, evaluation outputs, and conclusions
|-- src/             # Reusable helpers when needed
|-- .gitignore
`-- README.md
```

## Notebook 00: Data understanding and validation

Open [00_data_understanding_and_validation.ipynb](notebooks/00_data_understanding_and_validation.ipynb) for the documented, reproducible initial review.

The notebook covers source integrity, shape and dtypes, parsed nulls versus literal `unknown` values, the target distribution, contact-history segments, prior-outcome cross-tabs, numeric ranges, duplicate checks, and prediction-time feature decisions. It preserves the distinction between unknown prior outcomes and failures, explicitly excludes `pdays` from primary models, and leaves the contact-count wrap-up optional.

All 11 code cells passed in two fresh Jupyter kernels, once from `notebooks/` and once from the project root, with identical outputs. The notebook contains the executed outputs and reports the Python and package versions. Raw-file hashes and source row order remained unchanged.

To reproduce it, select the portfolio's existing Python environment (`../.venv/Scripts/python.exe` from this project folder), then restart the notebook kernel and run all cells. No additional packages were installed. The notebook does not export cleaned data, create a train/test split, or fit a model. Its full-file descriptive summaries are not held-out model evaluation; the notebook documents that limitation for later work.

## Next step

Review Notebook 00 and the remaining feature-timing questions, then agree on a feature dictionary and chronological split before creating preprocessing or modeling notebooks. `data/processed/` and `src/` remain empty apart from Git placeholders.
