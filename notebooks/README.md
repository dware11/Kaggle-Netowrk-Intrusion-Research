# Notebook status

## Original Phase 2 notebook

The original April 15, 2025 Kaggle notebook has been recovered from project storage.

Historical filename:

```text
phase-2-kaggle_Final04152025.ipynb
```

The GitHub copy that previously appeared under that name was **0 bytes** and was removed during the repository cleanup. It was not the real notebook.

## What the recovered notebook confirms

The recovered notebook contains the historical Phase 2 workflow, including:

- chunked loading of CIC-DDoS2019 attack CSVs;
- benign / attack sampling;
- train/test dataset generation;
- label and feature preprocessing;
- class-distribution analysis;
- feature selection using Random-Forest importance, Chi-Square, and RFE;
- experiments with multiple feature subset sizes;
- Logistic Regression, Random Forest, KNN, Decision Tree, and XGBoost;
- classification reports, confusion matrices, and per-attack F1 comparisons.

## Why the notebook is not being treated as the final reproducible artifact

The notebook records useful historical results, but it also reflects a one-off Kaggle environment and exploratory research workflow. For example, the recovered first cell shows a dependency compatibility error between `imbalanced-learn` and the installed scikit-learn version around the optional SMOTE import.

The next pass should therefore create a **cleaned reproduction notebook or Python pipeline** that:

1. starts from a verified environment;
2. removes dead / exploratory cells;
3. uses fixed random seeds;
4. makes train-only preprocessing boundaries explicit;
5. saves results and selected features to versioned files;
6. can run from top to bottom without manual repair.

## Historical results policy

Historical notebook outputs may be used to explain the original research process, but they should be labeled **historical / not freshly reproduced** until the clean pipeline is run successfully.

The final repository should retain the historical notebook as an archive and add a separate cleaned notebook or script for the verified reproduction.
