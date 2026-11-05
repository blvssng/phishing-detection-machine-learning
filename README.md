# Phishing Detection with Machine Learning

A machine-learning project that classifies websites as phishing or legitimate. It explores how data-driven detection could support defensive security efforts in settings such as banking and FinTech.

> **Project status:** Data preparation is complete, and initial model comparisons have been run. Further checks on feature reliance and generalisability are still needed.

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

- **Label handling:** In the source data, label `1` means legitimate and label `0` means phishing. A new `is_phishing` column was created with `1` for phishing and `0` for legitimate, making phishing the positive class. Recall therefore represents the share of phishing sites correctly identified.
- **Quality checks:** Duplicate rows and missing values were checked; none were found, so all 235,795 rows were retained.
- **Feature selection:** Numeric columns were retained for modelling. Text fields such as the raw URL and domain, as well as the filename field documented as ignorable, were excluded.
- **Leakage prevention:** Both label columns were excluded from the model features.
- **Class balance:** The classes are moderately balanced (57.2% legitimate, 42.8% phishing). Precision and recall are reported to show the two types of classification error separately.

## Methodology

- The data was split into training (80%) and test (20%) sets using stratification to preserve the class proportions. A fixed random seed of `42` was used for reproducibility.
- Two baseline models were compared: logistic regression with feature scaling, and random forest.
- Evaluation was performed on the held-out test set using precision, recall, F1, PR-AUC and a confusion matrix.

## Results (initial model comparison)

Evaluated on a held-out test set of 47,159 URLs (20,189 phishing and 26,970 legitimate).

| Model | Phishing missed (of 20,189) | Legitimate wrongly flagged (of 26,970) |
|---|---:|---:|
| Logistic Regression | 5 | 0 |
| Random Forest | 0 | 0 |

Both models performed near-perfectly on this test set. Since the dataset is known to be highly separable, these results may overstate real-world performance. Further checks on feature reliance and validation beyond this dataset are needed before drawing conclusions about deployment.

## Workflow

1. Load and profile the data; check class balance, missing values and duplicates.
2. Clean the data and document preparation decisions.
3. Explore feature distributions and relationships.
4. Split the data into stratified training and test sets.
5. Train logistic regression and random forest baselines.
6. Evaluate on the held-out test set.
7. Review feature importance and summarise the results and limitations.

## Evaluation Notes and Limitations

- Accuracy alone can be misleading, so results should be interpreted alongside precision, recall, F1, PR-AUC and the confusion matrix.
- A strong result on this held-out split does not establish that the models will perform similarly on new data. The dataset's strong `URLSimilarityIndex` signal may contribute to high scores, and the models have not yet been validated on an independent or time-separated dataset.
- The analysis uses one public dataset, which may not represent current or evolving phishing techniques, including AI-assisted phishing.
- The dataset does not establish whether AI was used to create a particular phishing site. This project therefore does not make claims about AI causing changes in phishing activity.

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
└── images/        # saved charts
```

## Author

**Blessing Muchirahondo** — data professional based in Johannesburg, South Africa.
