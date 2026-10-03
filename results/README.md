# Results

This directory is reserved for **verified outputs from the reproducible rerun**.

No final winner is published here yet because the recovered historical notebook has not been rerun end-to-end in a clean environment.

## Planned outputs

After reproduction, this directory should contain artifacts such as:

```text
results/
├── model_comparison.csv
├── selected_features.csv
├── summary.md
└── figures/
    ├── aggregate_model_comparison.png
    ├── per_attack_f1.png
    ├── confusion_matrices/
    └── feature_overlap.png
```

## What the final comparison should answer

1. Which classifier performs best with no feature selection?
2. Which feature-selection method produces the strongest aggregate performance?
3. Does the best selector change depending on the classifier?
4. Which attack classes are hardest to distinguish?
5. Can a smaller feature set preserve comparable performance?
6. Which features repeatedly appear across selection methods?
7. What tradeoff exists between predictive performance, feature count, and model complexity?

## Reporting rules

Final claims should be based on the clean rerun and should include:

- exact feature-selection method;
- number of selected features;
- model and key parameters;
- random seed;
- accuracy;
- macro F1;
- weighted F1;
- per-class F1 / precision / recall;
- confusion matrix;
- training runtime where practical.

Historical Kaggle metrics should remain clearly labeled as historical and should never be silently mixed with fresh reproduction results.
