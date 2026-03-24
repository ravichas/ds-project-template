# Predicting Hospital Readmission Risk from Clinical Indicators
### BIFX-546: Machine Learning for Bioinformatics — Spring 2026

**Team Members:**
- Jane Smith (jsmith@hood.edu)
- Carlos Mendez (cmendez@hood.edu)

---

## 🎯 Project Goal

Can we predict 30-day hospital readmission risk from routine clinical measurements
(lab values, vitals, diagnoses) collected at the time of discharge?

We hypothesize that a combination of discharge lab values and comorbidity count is
predictive of readmission, and that logistic regression can identify the most influential
clinical features.

---

## 📊 Dataset

| Field | Details |
|---|---|
| **Name** | Diabetes 130-US Hospitals (1999–2008) |
| **Source** | UCI Machine Learning Repository |
| **URL** | https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008 |
| **Size** | ~100,000 patient encounters, 50 features |
| **Citation** | Strack, B. et al. (2014). Impact of HbA1c Measurement on Hospital Readmission Rates. *BioMed Research International*, 2014. |

The dataset contains inpatient encounter records including demographics, diagnoses,
lab results, medications, and a binary readmission outcome (`<30 days` vs. `NO`).

---

## 🧠 Techniques Used

| Phase | Technique | Course Week |
|---|---|---|
| EDA | Descriptive statistics (mean, median, std, IQR) | Week 5 |
| EDA | Distribution plots, correlation heatmap, bar charts | Week 3 |
| Analysis | Chi-square test of independence (readmission vs. diagnosis group) | Week 6 |
| Analysis | Bootstrap confidence intervals on readmission rate | Week 6 |
| Modeling | Logistic Regression with train/test split (80/20) | Week 10 |
| Modeling | Decision Tree for feature importance comparison | Week 11 |
| Evaluation | Accuracy, Precision, Recall, AUC-ROC | Week 10–11 |

---

## 📁 Repository Structure

```
diabetes-readmission/
├── notebooks/
│   ├── 01_eda.ipynb              # Data loading, cleaning, EDA
│   ├── 02_hypothesis_testing.ipynb  # Statistical tests
│   └── 03_modeling.ipynb         # Logistic regression + decision tree
├── data/
│   └── README_data.md            # Link to UCI source; raw file not included (>50MB)
├── results/
│   ├── fig1_readmission_by_age.png
│   ├── fig2_correlation_heatmap.png
│   ├── fig3_roc_curve.png
│   └── table1_model_metrics.csv
├── src/
│   └── preprocess.py             # Reusable cleaning functions
├── README.md
└── requirements.txt
```

---

## ⚙️ How to Run

### Option 1 — Google Colab (recommended, no install needed)

1. Open [Google Colab](https://colab.research.google.com)
2. Click **File → Open notebook → GitHub**
3. Paste this repo URL and select the notebook you want to run
4. Run the first cell to install dependencies:
   ```python
   !pip install -r requirements.txt
   ```
5. Run all cells: **Runtime → Run all**

> **Note:** The dataset is downloaded automatically in the first notebook cell from the
> UCI URL. No manual download required.

### Option 2 — Local Jupyter

```bash
# Clone the repo
git clone https://github.com/yourteam/diabetes-readmission.git
cd diabetes-readmission

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

Open notebooks in order: `01_eda.ipynb` → `02_hypothesis_testing.ipynb` → `03_modeling.ipynb`

---

## 📈 Key Results & Plots

| Figure | File | Description |
|---|---|---|
| Fig 1 | `results/fig1_readmission_by_age.png` | Readmission rate by age group (bar chart) |
| Fig 2 | `results/fig2_correlation_heatmap.png` | Correlation matrix of numeric clinical features |
| Fig 3 | `results/fig3_roc_curve.png` | ROC curve comparing logistic regression vs. decision tree |

**Model performance summary:**

| Model | Accuracy | Precision | Recall | AUC-ROC |
|---|---|---|---|---|
| Logistic Regression | 0.74 | 0.61 | 0.58 | 0.79 |
| Decision Tree | 0.70 | 0.57 | 0.62 | 0.74 |

---

## 📝 Summary of Findings

Our EDA revealed that readmission rates differ substantially across age groups, with
patients aged 70–80 showing the highest 30-day readmission rate (~14%). A chi-square
test confirmed a statistically significant association between primary diagnosis category
and readmission status (p < 0.001), and bootstrap confidence intervals placed the
overall readmission rate at 11.2% ± 0.4%.

The logistic regression model achieved an AUC-ROC of 0.79, outperforming the
decision tree (0.74). The three strongest predictors of readmission were number of
inpatient visits in the prior year, number of diagnoses recorded at discharge, and
HbA1c result. These findings suggest that care-transition planning — particularly for
high-comorbidity patients with prior hospitalizations — may be the highest-yield
intervention target. Limitations include the dataset's age (1999–2008) and the
exclusion of social determinants of health, which likely confound readmission risk.

---

## 📦 Dependencies

See `requirements.txt`. Core packages:

```
pandas>=1.5
numpy>=1.23
matplotlib>=3.6
seaborn>=0.12
scikit-learn>=1.2
scipy>=1.10
jupyter
```

---

## 📜 References

1. Strack, B., DeShazo, J.P., et al. (2014). Impact of HbA1c Measurement on Hospital
   Readmission Rates: Analysis of 70,000 Clinical Database Patient Records.
   *BioMed Research International*, Article ID 781670.
   https://doi.org/10.1155/2014/781670

2. UCI Machine Learning Repository. (2014). Diabetes 130-US Hospitals Dataset.
   https://archive.ics.uci.edu/dataset/296

3. Grus, J. (2019). *Data Science from Scratch* (2nd ed.). O'Reilly Media.

---

*BIFX-546 · Hood College · Spring 2026 · Dr. Sarangan Ravichandran*
