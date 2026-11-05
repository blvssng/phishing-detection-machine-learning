## Results (initial model comparison)

Evaluated on a held-out test set of 47,159 URLs (20,189 phishing and 26,970 legitimate).

| Model | Phishing missed (of 20,189) | Legitimate wrongly flagged (of 26,970) |
|---|---:|---:|
| Logistic Regression | 5 | 0 |
| Random Forest | 0 | 0 |

Both models performed near-perfectly on this test set. Since the dataset is known to be highly separable, these results may overstate real-world performance. Further checks on feature reliance and validation beyond this dataset are needed before drawing conclusions about deployment.

