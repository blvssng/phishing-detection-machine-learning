# Phishing Detection with Machine Learning

A machine-learning project that classifies websites as phishing or legitimate. It explores how data-driven detection could support defensive security efforts in settings such as banking and FinTech.

> **Project status:** Data preparation and initial model comparisons are complete. Further checks on feature reliance and generalisability are still needed.

## Interactive Dashboard

[Open the interactive dashboard](https://claude.ai/artifact/KVd1quP2wnz7hm2QQcm8Hx#no_universal_links) to explore the dataset, test-set model results, feature importance, and the effect of removing `URLSimilarityIndex`. The dashboard is hosted on Claude, so access may depend on its sharing settings.

### Dashboard previews

**Project overview and test-set results**

![Dashboard overview and test-set results](images/dashboard-overview.png)

**Model comparison and error-cost illustrations**

![Dashboard model comparison and error-cost illustrations](images/dashboard-results.png)

**Feature reliance and model sensitivity**

![Dashboard feature reliance and model sensitivity](images/dashboard-features.png)

## Research Question

Can models identify phishing websites from URL and webpage features, and which model catches the most phishing sites while keeping false alarms low?

**Supporting questions**
- Which features are most associated with phishing in this dataset?
- How do baseline models compare on precision, recall, F1 and PR-AUC?
- What is the trade-off between missing a phishing site and incorrectly flagging a legitimate one?

## Type of Analysis

- **Descriptive:** examining class balance, feature distributions and relationships in the data.
- **Predictive:** training classification models to predict whether a website is phishing or legitimate.

## Data

- **Dataset:** [PhiUSIIL Phishing URL Dataset](https://archive.ics.uci.edu/dataset/967/phiusiil+phishing+url+dataset) (Prasad & Chandra, 2024), obtained from the UCI Machine Learning Repository.
- **Size:** 235,795 URLs: 134,850 legitimate (57.2%) and 100,945 phishing (42.8%).
- **Features:** 50 numeric features derived from URL structure and webpage characteristics.
- **Licence:** CC BY 4.0.
- **Citation:** Prasad, A. & Chandra, S. (2024). *PhiUSIIL Phishing URL (Website)* [Dataset]. UCI Machine Learning Repository.

## Data Preparation

- **Label handling:** In the source data, label `1` means legitimate and label `0` means phishing. A new `is_phishing` column was created with `1` for phishing and `0` for legitimate.
- **Quality checks:** Duplicate rows and missing values were checked; none were found, so all 235,795 rows were retained.
- **Feature selection:** Numeric columns were retained for modelling. Text fields such as the raw URL and domain, as well as the filename field documented as ignorable, were excluded.
- **Leakage prevention:** Both label columns were excluded from the model features.
- **Class balance:** The classes are moderately balanced (57.2% legitimate, 42.8% phishing). Precision and recall are reported to show the two types of classification error separately.

## Methodology

- The data was split into training (80%) and test (20%) sets using stratification to preserve the class proportions. A fixed random seed of `42` was used for reproducibility.
- Models compared: logistic regression with feature scaling, random forest, and random forest without `URLSimilarityIndex`.
- Evaluation was performed on the held-out test set. Error counts are shown below; performance metrics should be interpreted in light of the dataset limitations discussed later.

## Results

Evaluated on a held-out test set of 47,159 URLs (20,189 phishing and 26,970 legitimate).

| Model | Phishing missed (of 20,189) | Legitimate wrongly flagged (of 26,970) |
|---|---:|---:|
| Logistic Regression | 5 | 0 |
| Random Forest | 0 | 0 |
| Random Forest without `URLSimilarityIndex` | 6 | 4 |

![Top 10 feature importances](images/feature_importance.png)

## Key Findings

- Both models using all features performed near-perfectly on the test set: the random forest made no errors, while logistic regression missed 5 phishing URLs and wrongly flagged no legitimate URLs.
- Feature importance was distributed across multiple features. The most important included `URLSimilarityIndex`, `NoOfExternalRef`, `LineOfCode`, `NoOfSelfRef` and `NoOfImage`.
- After removing `URLSimilarityIndex`, the random forest made 10 errors in total: 6 phishing URLs were missed and 4 legitimate URLs were wrongly flagged. This corresponds to approximately 99.98% accuracy.
- In a banking context, the error types have different consequences: a missed phishing site presents a security risk, while a legitimate site wrongly flagged can inconvenience customers. The error costs shown in the dashboard are illustrative assumptions, not measured financial estimates.

## Limitations

- Scores this high likely overstate real-world performance. The data comes from a single public source, and legitimate and phishing pages may have been collected differently.
- Many of the strongest features describe webpage content, so they require fetching the page before a URL can be classified.
- The test set comes from the same collection as the training set, so it does not measure performance against new or AI-assisted phishing techniques.
- Feature importance indicates which features the model used; it does not show that those features cause a site to be phishing.

## Next Steps

- Test on a separate phishing dataset to check generalisation.
- Try URL-only features to simulate classifying a link before visiting it.
- Add model explainability (for example, SHAP) and a short comparison with other models.

## Workflow

1. Load and profile the data; check class balance, missing values and duplicates.
2. Clean the data and document preparation decisions.
3. Explore feature distributions and relationships.
4. Split the data into stratified training and test sets.
5. Train and compare baseline models.
6. Evaluate on the held-out test set.
7. Review feature importance and summarise results and limitations.

## Responsible Use

This is a defensive project focused on analysing and detecting phishing. It does not provide tools or instructions for carrying out attacks.

## AI Tools Disclosure

AI tools were used to assist with code and documentation. The analysis and outputs are reviewed and validated by the author.

## Repository Structure

```text
phishing-detection-machine-learning/
├── README.md
├── data/          # data notes; large raw files may be excluded
├── notebooks/     # exploration and modelling
├── src/           # reusable scripts
└── images/        # saved charts and dashboard screenshots
```

## Author

**Blessing Muchirahondo** — data professional based in Johannesburg, South Africa.
