# Experiment design

## Objective

The research question is broader than “which classifier has the highest accuracy?”

The experiment is designed to test how **feature-selection strategy and classifier choice interact** in a multiclass DDoS intrusion-detection problem.

The intended comparison is:

```text
feature-selection method × selected feature count × classifier
```

with both aggregate and per-attack metrics recorded for each configuration.

---

## Dataset scope

Dataset: **CIC-DDoS2019**

Historical Phase 2 classes:

1. BENIGN
2. DrDoS_DNS
3. DrDoS_LDAP
4. DrDoS_MSSQL
5. DrDoS_NTP
6. DrDoS_NetBIOS
7. DrDoS_SNMP
8. DrDoS_SSDP
9. DrDoS_UDP

The recovered notebook used eight DrDoS source files rather than every attack family available in the full CIC-DDoS2019 release.

---

## Historical preprocessing sequence

The recovered notebook shows the following broad workflow:

1. Read each attack CSV in chunks.
2. Sample benign and attack records from each file.
3. Combine the sampled records into a multiclass dataset.
4. Create training and test partitions.
5. Clean invalid, missing, and infinite values.
6. Encode categorical values and the target label.
7. Scale features where required by the selection/model method.
8. Apply feature selection.
9. Train the classifier.
10. Record aggregate and per-class metrics.

The reproduction version should convert these notebook steps into explicit functions or pipelines and ensure every learned preprocessing operation is fitted on training data only.

---

## Feature-selection methods

### 1. No-selection baseline

All cleaned candidate features are retained. This answers the essential baseline question:

> Does reducing the feature space actually improve performance, or does it only reduce complexity?

### 2. Random-Forest feature importance

A Random Forest is used to rank variables by importance, after which the top-ranked features are selected.

This is an **embedded/model-based** strategy capable of reflecting nonlinear relationships.

### 3. Chi-Square (`SelectKBest`)

The recovered notebook uses `SelectKBest(score_func=chi2, ...)` after Min-Max scaling to satisfy the Chi-Square method’s nonnegative-input requirement.

This is a **filter-based** approach: features are scored statistically before the final classifier is considered.

### 4. Recursive Feature Elimination (RFE)

The historical notebook uses Logistic Regression as the RFE estimator and recursively removes weaker features.

This is a **wrapper-style** strategy: feature usefulness is assessed in the context of a predictive model.

### Feature counts

The notebook contains experiments selecting **40 features** and later visual comparisons using **20 selected features**. The clean rerun should standardize the tested subset sizes across methods so each comparison is fair.

---

## Classifier matrix

The recovered Phase 2 notebook imports and evaluates:

- Logistic Regression
- Random Forest Classifier
- K-Nearest Neighbors (KNN)
- Decision Tree Classifier
- XGBoost Classifier

These models provide useful contrasts:

| Model | Research value |
| --- | --- |
| Logistic Regression | Linear baseline; useful for interpretability and RFE |
| KNN | Distance-based method; sensitive to scaling and feature space |
| Decision Tree | Simple nonlinear tree baseline |
| Random Forest | Ensemble tree model; robust nonlinear baseline and feature ranking |
| XGBoost | Boosted-tree model for stronger nonlinear classification |

---

## Metrics

The historical notebook records:

- Accuracy
- Per-class F1 score
- Weighted F1 score
- Precision
- Recall
- Confusion matrices / classification reports

### Primary interpretation rule

A final configuration should **not** be selected by accuracy alone.

The clean comparison should prioritize:

1. weighted F1 for aggregate multiclass performance,
2. macro F1 to expose class-level imbalance in performance,
3. per-class F1 and recall for individual attack families,
4. accuracy as a supporting metric,
5. number of retained features as a complexity / efficiency consideration.

Macro F1 should be added explicitly during reproduction even though the historical result table centered on per-class and weighted F1.

---

## Reproduction safeguards

The rerun should improve the original experimental hygiene in several ways:

- fix random seeds for sampling and model initialization where supported;
- split data before fitting scalers or feature selectors;
- fit preprocessing and feature selection on training data only;
- keep one untouched test partition for final evaluation;
- use the same feature-count candidates for each applicable selector;
- record runtime and selected feature names as well as predictive metrics;
- export all results to a single tidy CSV;
- pin dependency versions after the environment successfully runs end-to-end.

---

## Planned output schema

The reproduction results table should contain at least:

```text
feature_method
feature_count
model
attack_type
accuracy
macro_f1
weighted_f1
f1
precision
recall
training_seconds
random_seed
```

A separate feature-selection table should record the selected feature names for each method and feature count. That will make it possible to compare **feature overlap**, not only model scores.
