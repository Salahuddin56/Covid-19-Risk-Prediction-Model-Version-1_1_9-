# Covid-19-Risk-Prediction-Model-Version-1_1_9-
# 🦠 COVID-19 Patient Risk Prediction Model

> **BSc in Computer Science & Engineering — Thesis Project**
> American International University–Bangladesh (AIUB) | Spring 2023–2024

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Processing-green?logo=pandas)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![License](https://img.shields.io/badge/License-Academic-lightgrey)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Team](#team)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Methodology](#methodology)
- [Results](#results)
- [Installation](#installation)
- [Usage](#usage)
- [Known Issues & Fixes](#known-issues--fixes)
- [Limitations & Future Work](#limitations--future-work)
- [References](#references)

---

## Overview

The COVID-19 pandemic placed enormous strain on healthcare systems globally. Early identification of high-risk patients is critical for timely intervention and smart resource allocation. This project develops a **machine learning-based risk prediction model** that classifies COVID-19 patients into three risk levels — **Low**, **Medium**, and **High** — using clinical symptoms, diagnostic test results, and patient status data collected from real-world hospital records.

The project evaluates five classification algorithms:

| Algorithm | Category |
|---|---|
| Support Vector Machine (SVM) | Supervised |
| Naïve Bayes | Probabilistic |
| K-Nearest Neighbors (KNN) | Instance-based |
| Logistic Regression | Supervised |
| Decision Tree | Non-parametric Supervised |

---

## Team

| Name | Student ID |
|---|---|
| Salahuddin Elias Khan | 20-44139-2 |
| Swapnila Rumzum Das | 19-39439-1 |
| Niger Sultana Nishi | 19-40185-1 |
| Tasnia Tarannum Elma | 20-42686-1 |

**Supervised by:** Akinul Islam Jony
**Institution:** American International University–Bangladesh (AIUB)

---

## Dataset

- **Source:** Jessore Combined Military Hospital (CMH), Bangladesh — provided by Colonel Zinia Parveen, Deputy Commandant
- **Period:** January 2020 – August 2022
- **Original size:** 2,793 instances, 18 attributes
- **After cleaning:** 2,667 instances

### Attributes

| Column | Description |
|---|---|
| `S1: Fever` | Presence of fever symptom (binary) |
| `S2: Cough` | Presence of cough symptom (binary) |
| `S3: Joint Pain` | Presence of joint pain (binary) |
| `S4: Shortness of Breath` | Presence of breathing difficulty (binary) |
| `Test1: RAT` | Rapid Antigen Test result (dropped — positive for all) |
| `Test2: RT PCR` | RT-PCR test result (binary) |
| `Test3: Chest X Ray` | Chest X-Ray result (binary) |
| `Test4: CT Scan` | CT Scan result (binary) |
| `Age` | Patient age (converted → Age Range categories) |
| `Status` | Patient admission/discharge status |
| `Risk Factor` | **Target variable** — Low / Medium / High |

### Risk Factor Distribution
High    →  393
Medium  →  696
Low     → 1578

---

## Project Structure
covid-risk-prediction/
│
├── data/
│   └── Final-Data-COVID-PATIENT-STATE-2020-2022-dirty-data2.xlsx
│
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_eda.ipynb
│   └── 03_model_training_evaluation.ipynb
│
├── src/
│   └── covid_risk_prediction.py      # Main script
│
├── outputs/
│   ├── accuracy_bar_chart.png
│   ├── correlation_heatmap.png
│   ├── pairplot.png
│   └── parallel_coordinates.png
│
├── requirements.txt
└── README.md

---

## Methodology

### 1. Data Collection

Raw data was obtained from Jessore CMH in mixed formats — some digital (`.doc`) and some handwritten. Handwritten records were digitized using an iPhone image-to-text scanner and then converted to `.csv`/`.xlsx`.

### 2. Data Preprocessing

Cleaning was performed in four steps:

1. **Step 1 — Drop missing status rows:** 15 rows dropped (sensitive data, cannot impute)
2. **Step 2 — Fix age format:** Convert `Age` column to numeric; 115 additional rows dropped
3. **Step 3 — Remove duplicates:** Duplicate rows dropped
4. **Step 4 — Age categorization:** Age converted to ranges and one-hot encoded

| Age Range | Range |
|---|---|
| Children | 1–12 |
| Adolescents | 13–17 |
| Adults | 18–64 |
| Elders | 65–100 |

Dropped columns deemed unnecessary:
- `Date of Admission`
- `Date of Discharge`
- `Date of Expired`
- `Test1: RAT` (positive for all patients — no discriminative value)

Missing values in feature columns were imputed using the **median strategy**.

### 3. Exploratory Data Analysis (EDA)

- **Countplot** — class distribution by risk factor
- **Correlation Heatmap** — inter-variable relationships
- **Pairplot** — pairwise attribute visualizations colored by risk class
- **Parallel Coordinates Plot** — multi-dimensional feature patterns

Notable correlations:
- `Status` ↔ `Test4: CT Scan`: 0.78 (strong)
- `Status` ↔ `Test3: Chest X Ray`: 0.59 (moderate)
- `Test3: Chest X Ray` ↔ `Test4: CT Scan`: 0.44 (moderate)

### 4. Feature Matrix (X)

```python
X = df[['S1: Fever', 'S2: Cough', 'S3: Joint Pain',
        'Test2:RT PCR', 'Test3: Chest X Ray', 'Test4: CT Scan', 'Status']]
```

### 5. Target Variable (y)

```python
y = df['Risk Factor']  # Low / Medium / High
```

### 6. Train/Test Split
Training set : 72%  (1,920 samples)
Test set     : 28%  (747 samples)
random_state = 16

---

## Results

### Test Set Accuracy

| Algorithm | Accuracy |
|---|---|
| Decision Tree | **88.09%** ✅ |
| KNN | 81.39% |
| Logistic Regression | 79.92% |
| SVM | 74.42% |
| Naïve Bayes | 71.22% |

The **Decision Tree** classifier achieved the highest accuracy at **88.09%** and was identified as the best-performing model on this dataset.

> Note: Slight differences between the output shown in the thesis (section 5) and the table in section 5.1 are due to rounding and different evaluation runs.

---

## Installation

### Prerequisites

- Python 3.10+
- pip

### Setup

```bash
# Clone the repository
git clone https://github.com/your-username/covid-risk-prediction.git
cd covid-risk-prediction

# Install dependencies
pip install -r requirements.txt
```

### `requirements.txt`
pandas
numpy
matplotlib
seaborn
scikit-learn
openpyxl
---

## Usage

### Run the full pipeline

```bash
python src/covid_risk_prediction.py
```

Make sure the dataset file `Final-Data-COVID-PATIENT-STATE-2020-2022-dirty-data2.xlsx` is placed in the `data/` folder (or update the file path in the script).

### Key Code Sections

**Data loading:**
```python
df = pd.read_excel('data/Final-Data-COVID-PATIENT-STATE-2020-2022-dirty-data2.xlsx')
```

**Model training & evaluation:**
```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.28, random_state=16)

model_dt = DecisionTreeClassifier()
model_dt.fit(X_train, y_train)
y_pred_dt = model_dt.predict(X_test)
print(metrics.accuracy_score(y_test, y_pred_dt))
```

**5-fold Cross-validation:**
```python
cv_scores = cross_val_score(model, X, y, cv=5)
print(f"CV Accuracy: {np.mean(cv_scores)*100:.2f}%")
```

---

## Known Issues & Fixes

### ❌ `TypeError: '<' not supported between instances of 'float' and 'str'`

**Cause:** The target variable `y = df['Risk Factor']` contains a mix of `float` and `str` values due to dirty data. When `cross_val_score` tries to determine the target type via `numpy.unique()`, it fails because the array has mixed types.

**Fix:** Clean the target variable before use:

```python
# Drop rows where 'Risk Factor' is NaN or non-string
df = df[df['Risk Factor'].notna()]
df['Risk Factor'] = df['Risk Factor'].astype(str).str.strip()

# Re-assign after cleaning
y = df['Risk Factor']
```

Also ensure the index is reset after filtering:

```python
df = df.reset_index(drop=True)
X = X.reset_index(drop=True)
y = y.reset_index(drop=True)
```

> **Root cause in the original code:** `X['Status'] = pd.to_numeric(df['Status'], errors='coerce')` was re-assigning from the original `df` instead of the already-processed `X`, which introduced index misalignment. Use `X['Status'] = pd.to_numeric(X['Status'], errors='coerce')` instead.

---

## Limitations & Future Work

1. **Dataset size** — The model was trained on ~2,667 records. Larger datasets (10,000+ records) would significantly improve model generalizability and push accuracy beyond 90–95%.

2. **Class imbalance** — The Low risk class (1,578) dominates over High (393). Techniques like SMOTE or class weighting should be explored.

3. **Feature richness** — Additional clinical features (comorbidities, blood oxygen levels, lab biomarkers) would improve prediction quality.

4. **Model complexity** — Deep learning approaches (LSTM, Transformer-based models on EHR sequences) could be explored in future iterations.

5. **Cross-population generalizability** — The model was trained on Bangladeshi military hospital data and may not generalize to other demographics or healthcare systems without retraining.

6. **Medical domain knowledge** — Future developers working with medical datasets should have baseline clinical knowledge to interpret data patterns meaningfully.

---

## References

1. Wynants L, et al. *Prediction models for diagnosis and prognosis of COVID-19 infection: systematic review and critical appraisal.* BMJ. 2020;369:m1328.
2. Yan L, et al. *An interpretable mortality prediction model for COVID-19 patients.* Nat Mach Intell. 2020;2:283-288.
3. Li X, et al. *Machine learning models can early predict hypertensive patients with severe COVID-19.* J Med Internet Res. 2021;23(2):e25984.
4. Farid SS, et al. *Developing a machine learning model for predicting COVID-19 severity in Iran.* J Med Syst. 2021;45(3):28.
5. Gupta A, et al. *Extrapulmonary manifestations of COVID-19.* Nat Med. 2020;26(7):1017-1032.
6. Chowdhury MEH, et al. *Can AI help in screening viral and COVID-19 pneumonia?* IEEE Access. 2020;8:132665-132676.
7. Ribeiro MH, et al. *Can machine learning predict COVID-19 pneumonia severity using chest x-ray imaging?* Eur Radiol. 2020;30(12):6774-6781.

---

## Acknowledgements

Special thanks to **Colonel Zinia Parveen**, Deputy Commandant of Jessore CMH, for providing the real-world COVID-19 patient dataset that made this research possible.

---

*Submitted: 12th June 2023 | AIUB Spring 2023–2024*
