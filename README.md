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
