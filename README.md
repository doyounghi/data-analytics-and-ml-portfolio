# Data Analytics and Machine Learning Portfolio

This repository contains Python portfolio projects in data analytics, machine learning, and experimentation across healthcare and banking. The work covers member analytics, randomized outreach evaluation, cost modeling, readmission-risk prioritization, and bank-marketing contact-history analysis.

The projects use **synthetic healthcare-style datasets** and **public datasets from healthcare and banking**. Results are intended for portfolio, learning, and demonstration purposes. They should not be interpreted as validated clinical, operational, or financial recommendations.

## Recommended Review Path

For a fast review, start here:

| Review Goal | Recommended File |
| :--- | :--- |
| **Best Machine Learning Workflow** | `03_risk_stratification_intervention_prioritization/notebooks/05_model_comparison_and_threshold_strategy.ipynb` |
| **Best Risk Modeling Setup** | `03_risk_stratification_intervention_prioritization/notebooks/04_baseline_risk_modeling.ipynb` |
| **Best Statistical Analysis** | `02_diabetes_peer_support_ab_testing/notebooks/02_ab_test_primary_outcome.ipynb` |
| **Best Business Recommendation** | `02_diabetes_peer_support_ab_testing/notebooks/06_Business_Recommendation_Summary.ipynb` |
| **Bank Marketing Data Understanding** | [Notebook 00: Data understanding and validation](04_bank_marketing_history_segmentation/notebooks/00_data_understanding_and_validation.ipynb) |

This path highlights patient-aware readmission modeling, threshold-based outreach prioritization, randomized experiment analysis, business recommendations, and reproducible data understanding. The bank-marketing project is in progress; Notebook 00 is complete, and no model has been trained for that project.

## Projects

### 01 — Synthetic Medicaid & Medicare Member Analytics

End-to-end healthcare analytics and machine learning project using synthetic Medicaid/Medicare-style member-level data.

This project demonstrates member-level healthcare analytics, Annual Wellness Visit completion modeling, monthly cost regression, model interpretation, and final project synthesis.

Main topics:

* Synthetic healthcare member data generation
* Medicaid/Medicare-style member analytics
* Annual Wellness Visit completion classification
* Monthly healthcare cost regression
* Feature engineering
* Model comparison
* Residual diagnostics
* Tree-based models
* Random Forest and Gradient Boosting
* Hyperparameter tuning
* Portfolio-ready project summary

Key files:

* `01_medicare_and_medicaid_member_analysis/README.md`
* `01_medicare_and_medicaid_member_analysis/notebooks/15_final_regression_model_comparison.ipynb`
* `01_medicare_and_medicaid_member_analysis/notebooks/16_project_summary.ipynb`

---

### 02 — Diabetes Peer Support A/B Testing and Outreach Evaluation

Healthcare experimentation project evaluating whether a Diabetes Peer Support outreach program improves diabetes testing compliance compared with Standard Outreach.

This project uses a synthetic randomized experiment design and follows an **intent-to-treat** framework. Members are analyzed based on randomized assignment rather than later enrollment or attendance behavior.

The primary outcome notebook focuses on treatment-effect estimation. The funnel notebook is operational: it evaluates outreach execution, drop-off, and participation flow after assignment.

Main topics:

* Synthetic healthcare outreach data generation
* Randomized treatment/control assignment
* Intent-to-treat A/B testing
* Baseline balance validation
* Standardized mean differences
* Two-proportion z-test
* Welch's t-test
* Absolute lift and relative lift
* Confidence intervals and p-values
* Peer-support funnel analysis
* SDOH segment analysis
* Adjusted regression sensitivity analysis
* Logistic regression and odds ratios
* Business recommendation summary

Key notebooks:

* `02_diabetes_peer_support_ab_testing/notebooks/01_EDA_And_Randomization_Balance_Check.ipynb`
* `02_diabetes_peer_support_ab_testing/notebooks/02_ab_test_primary_outcome.ipynb`
* `02_diabetes_peer_support_ab_testing/notebooks/03_Peer_Support_Funnel_Analysis.ipynb`
* `02_diabetes_peer_support_ab_testing/notebooks/04_SDOH_Segment_Analysis.ipynb`
* `02_diabetes_peer_support_ab_testing/notebooks/05_adjusted_sensitivity_analysis.ipynb`
* `02_diabetes_peer_support_ab_testing/notebooks/06_Business_Recommendation_Summary.ipynb`

---

### 03 — Readmission Risk Stratification and Outreach Prioritization

Healthcare risk modeling project using the public UCI Diabetes 130-US Hospitals dataset to predict 30-day hospital readmission risk and translate predicted risk scores into a capacity-constrained outreach prioritization strategy.

This project is framed around a practical care-management question:

> How can a care management team identify high-risk encounters, rank them by predicted readmission risk, and prioritize limited outreach capacity?

The project uses encounter-level hospital data and includes leakage-aware feature engineering, patient-aware validation, baseline modeling, model comparison, and threshold strategy.

Main topics:

* Public de-identified healthcare dataset analysis
* 30-day readmission target creation
* Real-world missing-value handling
* Encounter-level vs patient-level unit-of-analysis review
* Patient-aware train/test splitting
* Leakage-aware feature selection
* Near-discharge prediction framing
* Feature engineering for utilization, diagnosis, medication, and missingness patterns
* Baseline Logistic Regression and Decision Tree modeling
* Candidate model comparison with Logistic Regression, Random Forest, and Gradient Boosting
* ROC AUC and PR AUC evaluation
* Grouped cross-validation
* Top 5%, Top 10%, and Top 20% risk-group analysis
* Lift over baseline
* Precision at k and recall at k
* Outreach capacity simulation
* Risk tier creation
* Threshold strategy for care management prioritization
* Calibration and causal interpretation caution
* Subgroup performance and selection-pattern review
* Encounter-level versus patient-level outreach planning

Key notebooks:

* `03_risk_stratification_intervention_prioritization/notebooks/00_project_setup_and_data_access_check.ipynb`
* `03_risk_stratification_intervention_prioritization/notebooks/01_data_cleaning_and_dictionary.ipynb`
* `03_risk_stratification_intervention_prioritization/notebooks/02_eda_and_outcome_analysis.ipynb`
* `03_risk_stratification_intervention_prioritization/notebooks/03_feature_engineering_and_leakage_review.ipynb`
* `03_risk_stratification_intervention_prioritization/notebooks/04_baseline_risk_modeling.ipynb`
* `03_risk_stratification_intervention_prioritization/notebooks/05_model_comparison_and_threshold_strategy.ipynb`
* `03_risk_stratification_intervention_prioritization/notebooks/06_fairness_and_subgroup_review.ipynb`
* `03_risk_stratification_intervention_prioritization/notebooks/07_intervention_prioritization_and_business_recommendation.ipynb`

---

### 04 - Bank Marketing: Contact History and Campaign Prioritization

An in-progress banking analytics project using the original UCI Bank Marketing dataset to study term-deposit subscription and prior-campaign contact history.

The intended decision point is before the first call of the current campaign. The planned comparison is between a pooled common-feature model, a pooled model with verified history features, and separate models for clients with and without prior-campaign contact history.

**Current status:** Notebook 00 is complete and executed. It documents 45,211 records, the target distribution, missing-information categories, contact-history segments, prior-outcome consistency, duplicate checks, and feature-timing limitations. No model has been trained.

Main topics:

* Reproducible data understanding and source verification
* No-prior-contact versus prior-contact segmentation using `previous`
* Unknown prior outcomes distinguished from failures
* Pre-first-call feature availability and leakage prevention
* `pdays` and final/current-campaign contact fields excluded from primary models
* Shared chronological evaluation design for the planned model comparison
* Observational and causal interpretation limits

Key files:

* [Project overview](04_bank_marketing_history_segmentation/README.md)
* [Notebook 00: Data understanding and validation](04_bank_marketing_history_segmentation/notebooks/00_data_understanding_and_validation.ipynb)
* [Dataset source and validation manifest](04_bank_marketing_history_segmentation/reports/source_manifest.json)

These are contact-history segments, not new versus existing bank customers. The project does not estimate the causal effect of making a call.

## Skills Demonstrated

**Languages and libraries:** Python, pandas, NumPy, matplotlib, scipy, statsmodels, scikit-learn

**Healthcare analytics:** Medicaid/Medicare-style member analytics, Annual Wellness Visit analytics, diabetes testing compliance, readmission risk, outreach prioritization, SDOH segment analysis

**Machine learning:** Feature engineering, classification modeling, regression modeling, model comparison, tree-based models, grouped train/test splitting, grouped cross-validation, ROC AUC, PR AUC, precision, recall, lift analysis, threshold strategy

**Experimentation and statistics:** Intent-to-treat A/B testing, baseline balance checks, standardized mean differences, two-proportion z-test, Welch's t-test, confidence intervals, p-values, logistic regression, odds ratio interpretation

**Business analytics:** Funnel analysis, subgroup analysis, risk tiering, outreach capacity simulation, contact-history segmentation, business recommendation development, data storytelling, Git/GitHub project organization

**Data understanding and reproducibility:** Source documentation, data validation, missing-value interpretation, duplicate and unit-of-analysis review, feature-timing decisions, and executed notebooks

## Repository Structure

```text
data-analytics-and-ml-portfolio/
|
|-- 01_medicare_and_medicaid_member_analysis/
|   |-- notebooks/
|   |-- data/
|   |-- src/
|   |-- requirements.txt
|   `-- README.md
|
|-- 02_diabetes_peer_support_ab_testing/
|   |-- notebooks/
|   |-- data/
|   |-- src/
|   |-- requirements.txt
|   `-- README.md
|
|-- 03_risk_stratification_intervention_prioritization/
|   |-- notebooks/
|   |-- data/
|   |-- outputs/
|   |-- src/
|   |-- requirements.txt
|   `-- README.md
|
|-- 04_bank_marketing_history_segmentation/
|   |-- notebooks/
|   |-- data/
|   |-- reports/
|   |-- src/
|   `-- README.md
|
`-- README.md
```

Start with each project's README for its dataset, setup, and interpretation notes. Raw source files excluded by project ignore rules must be obtained separately from the documented sources.

## About the Author

I am a healthcare data analyst focused on Medicaid/Medicare analytics, population health reporting, quality improvement, and risk stratification workflows.

My professional work includes SQL, Power BI, DAX, Excel, and healthcare dashboard development. This repository focuses on Python-based analytics and machine learning workflows that complement that business intelligence background.

I am also pursuing graduate-level analytics training through Georgia Tech OMSA.

LinkedIn: [Doyoung Kim](https://www.linkedin.com/in/doyoung-kim-hello/)

## Notes on Interpretation

These projects are portfolio demonstrations, not production decision tools.

Model predictions, experiment results, and business recommendations demonstrate analytical workflow design, statistical reasoning, and business interpretation. Synthetic experiment results do not establish real-world treatment effects, and observational prediction does not establish that an outreach action causes a better outcome. These projects should not be used for real clinical, financial, or operational decisions without external validation, governance review, and appropriate deployment controls.
