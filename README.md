# Phishing Detection with Machine Learning

A machine learning project that classifies websites as phishing or legitimate, with a focus on how AI-based detection can support banks and FinTech firms, where phishing is a common route for fraud and account compromise.

> **Project status:** In progress. Results will be added once the analysis is complete. This README describes the plan, not finished findings.

## Research Question

Can a model identify phishing websites from their features, and which model catches the most phishing while keeping false alarms low?

**Supporting questions**
- Which features are most associated with phishing?
- How do several baseline models compare on precision, recall and F1?
- What is the trade-off between missing a phishing site and wrongly blocking a legitimate one?

## Type of Analysis

- **Descriptive:** exploring the data (class balance, feature distributions, correlations) to understand what has been observed.
- **Predictive (main approach):** training classification models to predict whether a site is phishing.

## Data

- A public phishing website dataset (for example the UCI Phishing Websites dataset, or a phishing URL dataset from Kaggle).
- The final README will record the exact source, link, licence, row count, class balance and any cleaning applied.

**Data elements needed**
- Label: phishing or legitimate
- URL-based features (length, number of special characters, use of IP address, number of subdomains)
- Page or domain features available in the chosen dataset (HTTPS use, domain age, redirects)

## Tools

Python (pandas, scikit-learn, matplotlib, seaborn), Jupyter Notebook, Git and GitHub.

## Workflow

1. Load and profile the data; check class balance and missing values.
2. Clean the data and document each decision.
3. Explore feature distributions and correlations.
4. Split into training and test sets (stratified).
5. Train baseline models (logistic regression, random forest) and compare.
6. Evaluate with precision, recall, F1, PR-AUC and a confusion matrix.
7. Review feature importance and summarise limitations.

## Repository Structure

```text
phishing-detection-ml/
├── README.md
├── data/          # data notes; large raw files may be excluded
├── notebooks/     # exploration and modelling
├── src/           # reusable scripts
└── images/        # saved charts
```

## Evaluation Notes

- Accuracy alone can mislead, so results will be reported with precision, recall, F1 and the confusion matrix.
- Models are tested on a held-out test set that is not used during training.
- Results reflect one public dataset and may not generalise to new or evolving phishing techniques.

## Limitations

- Public datasets may be outdated and may not reflect current attacker methods, including AI-assisted phishing.
- The data cannot show whether AI was used to create a given phishing site, so this project does not claim that AI caused any change in attack volumes.

## Responsible Use

This is a defensive project: it analyses and detects phishing. It contains no tools or instructions for carrying out attacks.

## AI Tools Disclosure

AI tools were used to assist with code and documentation. All analysis was reviewed and validated by the author.

## Findings

*To be added after the analysis is complete.*

## Author

**Blessing Muchirahondo** — data professional based in Johannesburg, South Africa.
