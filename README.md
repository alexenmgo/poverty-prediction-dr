# 🇩🇴 Monetary Poverty Prediction in the Dominican Republic
### Using Multidimensional Variables & Machine Learning

> **Master's Thesis — M.Sc. in Data Science**  
> Instituto Tecnológico de Santo Domingo (INTEC) · 2023  
> **Author:** Alexis Enmanuel Gómez · **Advisor:** Renato González

---

## 📌 Overview

Traditional poverty measurement in the Dominican Republic relies exclusively on monetary income, which fails to capture the full complexity of deprivation. This project uses **multidimensional socioeconomic variables** — aligned with the SIUBEN Multidimensional Poverty Index (IPM-RD) — combined with **supervised machine learning algorithms** to predict and classify monetary poverty among Dominican households.

The study analyzes data across three time periods to account for the effects of COVID-19:
- **2018–2019** — Pre-pandemic
- **2021–2022** — Post-pandemic
- **All periods combined**

---

## 📊 Dataset

| Detail | Value |
|--------|-------|
| **Source** | ENCFT — National Continuous Labor Force Survey, Central Bank of DR |
| **Years** | 2018, 2019, 2021, Q1–Q3 2022 |
| **Records** | 164,737 households |
| **Features** | 15 independent variables |
| **Target variables** | `Pobre` (general poverty) · `Indigente` (extreme poverty) |
| **Train / Test split** | 70% / 30% |
| **Class imbalance treatment** | Random Oversampling (SMOTE-style) |

---

## 🧮 Features — Based on SIUBEN IPM-RD Methodology

All variables are binary (1 = deprived, 0 = not deprived):

| Variable | Deprivation Definition |
|----------|----------------------|
| `HACINAMIENTO` | 3+ persons per bedroom |
| `rezago_educativo` | At least one household member 2+ years behind grade level |
| `seguro_medico` | At least one member without health insurance |
| `sustento_hogar` | No employed adult (18+) in the household |
| `logro_educativo` | Educational attainment below age-appropriate threshold |
| `inasistencia_escolar` | At least one child (5–20) not attending school |
| `informalidad` | At least one working-age member without pension contribution |
| `Material_vivienda` | Substandard floor, walls, or roof materials |
| `Agua_potable` | No piped water or less than 4x/week access |
| `Saneamiento` | No sanitation or shared sanitation facilities |
| `Combustible` | Cooks with charcoal, wood, or non-approved fuel |
| `Electricidad` | Uses kerosene or propane lamp lighting |
| `BRECHA_DIGITAL` | No computer, phone, or internet-connected tablet |
| `trabajo_infantil` | Child labor (ages 5–17) |
| `ZONA` | Control variable: 1 = urban, 2 = rural |

---

## 🤖 Models Evaluated

- Logistic Regression
- **Random Forest** ← Best for general poverty
- Support Vector Machines (SVM)
- XGBoost
- **Neural Networks** ← Best for extreme poverty

---

## 📈 Results

### General Poverty Classification

| Model | Accuracy | Recall | Precision | F1 | AUC |
|-------|----------|--------|-----------|-----|-----|
| Logistic Regression | 0.705 | 0.659 | 0.433 | 0.522 | 0.65 |
| **Random Forest** | **0.740** | **0.671** | **0.477** | **0.558** | **0.72** |
| SVM | 0.706 | 0.658 | 0.434 | 0.523 | 0.69 |
| XGBoost | 0.730 | 0.674 | 0.464 | 0.550 | 0.64 |
| Neural Networks | 0.711 | 0.704 | 0.443 | 0.544 | 0.71 |

> ✅ **Best model:** Random Forest (2018–2019) — correctly classifies **67% of poor households**

---

### Extreme Poverty (Indigence) Classification

| Model | Accuracy | Recall | F1 | AUC |
|-------|----------|--------|----|-----|
| Logistic Regression | 0.767 | 0.729 | 0.175 | 0.60 |
| Random Forest | 0.817 | 0.783 | 0.226 | 0.80 |
| SVM | 0.783 | 0.703 | 0.181 | 0.74 |
| XGBoost | 0.818 | 0.775 | 0.225 | 0.80 |
| **Neural Networks** | **0.844** | **0.731** | **0.242** | **0.80** |

> ✅ **Best model:** Neural Networks (2018–2019) — predicts **73% of extremely poor households**

---

## 🔑 Most Influential Variables

### For General Poverty (Random Forest — Top 5)
1. 🏠 **Overcrowding** (hacinamiento) — strongest predictor
2. 📚 Educational lag (rezago educativo)
3. 🏥 Health insurance (seguro médico)
4. 💼 Household sustenance (sustento del hogar)
5. 🎓 Educational attainment (logro educativo)

### For Extreme Poverty (Neural Networks — Top 5)
1. 💼 **Household sustenance** — strongest predictor
2. 🏠 Overcrowding (hacinamiento)
3. 🏥 Health insurance (seguro médico)
4. 📚 Educational lag (rezago educativo)
5. 🎓 Educational attainment (logro educativo)

---

## 💡 Key Findings

- Multidimensional variables successfully classify **67% of monetarily poor** and **73% of extremely poor** households — without using income data
- Models performed better in **pre-pandemic periods (2018–2019)**, suggesting COVID-19 introduced structural changes not captured by traditional indicators
- **Overcrowding** is the single strongest predictor of general poverty; **lack of household income earner** is the strongest for extreme poverty
- All models achieved **AUC > 0.5**, confirming discrimination ability above random chance
- Results support CEPAL's argument that income-only poverty measures are insufficient and multidimensional approaches yield more actionable insights for public policy

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-Gradient%20Boosting-green)
![Google Colab](https://img.shields.io/badge/Google%20Colab-Notebook-yellow)
![R](https://img.shields.io/badge/R-Poverty%20Calculation-lightblue)

- **Python** — modeling, feature engineering, evaluation metrics
- **Scikit-learn** — Logistic Regression, Random Forest, SVM, Neural Networks
- **XGBoost** — gradient boosting classifier
- **R** — monetary poverty calculation using MEPYD official methodology
- **Google Colab** — development environment

---

## 📓 Notebooks

| Notebook | Period | Target |
|----------|--------|--------|
| [Poverty 2018–2019](https://colab.research.google.com/drive/1D_4NUKWyk7tT67zYJwN9Qaj9A7kAMMrb) | Pre-pandemic | General poverty |
| [Poverty 2021–2022](https://colab.research.google.com/drive/1KZJM4SOTkMhEkIGEF2yacuv6ZQxcEffD) | Post-pandemic | General poverty |
| [Poverty All Periods](https://colab.research.google.com/drive/1uypkjhzk2vrqVC6Tk1x-EFk2jXZ-G1zB) | Combined | General poverty |
| [Indigence 2018–2019](https://colab.research.google.com/drive/1x6xGe4TcHhMbkXOoDFZ0gJk_uhtjIW9) | Pre-pandemic | Extreme poverty |
| [Indigence 2021–2022](https://colab.research.google.com/drive/1VPVeWRQUu2sJCbpoOB1Ak2IHWrj3Rgy) | Post-pandemic | Extreme poverty |
| [Indigence All Periods](https://colab.research.google.com/drive/14wHJO_Ty-VbTHE6an4rzyI1kBCGMaPy) | Combined | Extreme poverty |

---

## 📋 References

- Alkire, S. & Foster, J. (2009). *Counting and multidimensional poverty measurement*. Oxford.
- Breiman, L. (2001). *Random Forests*. Statistics Department, UC Berkeley.
- CEPAL (2013). *La medición multidimensional de la pobreza*.
- MEPYD — Ministerio de Economía, Planificación y Desarrollo, Dominican Republic.
- SIUBEN — Sistema Único de Beneficiarios, IPM-RD 2017.

---

*This research contributes to the evidence base for multidimensional poverty measurement in the Dominican Republic and provides a foundation for more targeted and effective public policy design.*
