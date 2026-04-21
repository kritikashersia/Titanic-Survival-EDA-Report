# Titanic Dataset — Exploratory Data Analysis

A complete exploratory data analysis (EDA) of the Titanic passenger dataset,
answering the question: **Who survived, and why?**

This project walks through the standard EDA workflow — data loading, cleaning,
feature engineering, visualization, and narrative reporting — using pandas,
matplotlib, and seaborn.

---

## Project Overview

The Titanic sank on April 15, 1912, killing over 1,500 of its ~2,200
passengers and crew. Survival was not random: it tracked patterns in sex,
social class, age, and family structure. This project uses a 891-passenger
sample to uncover those patterns through exploratory analysis.

**Goal:** Produce a clean, reproducible EDA that a non-technical reader
can follow — from raw CSV to a 300-word narrative of findings.

---

## Repository Structure
titanic-eda/
├── titanic.csv                  # Raw dataset (891 passengers, 15 columns)
├── titanic_eda.ipynb            # Main analysis notebook
├── titanic_cleaned.csv          # Cleaned dataset (output)
├── matplotlib_overview.png      # 4-panel summary figure
├── heatmap.png                  # Correlation heatmap
├── violin_age.png               # Age distribution by survival
└── README.md                    # You are here

## 🔍 Analysis Workflow

The notebook follows a six-step EDA pipeline:

### Step 1 — Load & Inspect
Load the CSV, check shape (891 × 15), inspect data types with `.info()`,
summary stats with `.describe()`, and locate missing values.

### Step 2 — Handle Missing Values
Three columns had gaps, each handled by a different strategy:

| Column | Missing | Strategy |
|---|---|---|
| `Cabin` (deck) | 688 (77%) | **Dropped** — too sparse |
| `Age` | 177 (20%) | **Filled with median** (28.0) |
| `Embarked` | 2 (0.2%) | **Filled with mode** (S) |

### Step 3 — Feature Engineering
Two new features derived from existing columns:
- `FamilySize = SibSp + Parch + 1` — total party size
- `IsAlone` — binary flag for solo travellers

### Step 4 — Matplotlib Visualizations
A 2×2 figure showing survival by sex, survival by class,
age distribution, and family-size effects.

### Step 5 — Seaborn Visualizations
- **Correlation heatmap** — numeric relationships across features
- **Split violin plot** — age distribution by survival and sex

### Step 6 — Narrative Summary
A 300-word written summary interpreting the findings.

---

## Key Findings

> **Of 891 passengers, 342 (38.4%) survived.**

| Factor | Finding |
|---|---|
| **Sex** | Women: **74.2%** survived · Men: **18.9%** |
| **Class** | 1st: **63.0%** · 2nd: **47.3%** · 3rd: **24.2%** |
| **Sex × Class** | 1st-class woman: **96.8%** · 3rd-class man: **13.5%** |
| **Age** | Children (0–12): **58.0%** · Seniors (60+): **22.7%** |
| **Family size** | Alone: **30.4%** · Small families (2–4): **55–72%** · Large (5+): ~16% |

**Top linear correlates of survival:**
`Pclass` (r = −0.34) · `Fare` (r = +0.26) · `IsAlone` (r = −0.20)

---

## Main Takeaway

The archetypal **survivor** was a first- or second-class woman travelling
with a small family, or a child of either sex. The archetypal **victim**
was a third-class man travelling alone. The tragedy was shaped less by
chance than by the social hierarchy and physical layout of the ship —
the "women and children first" protocol combined with cabin locations
that determined how quickly passengers could reach the lifeboats.

---

## Limitations

- Imputing 177 missing ages with the median creates an artificial spike
  near age 28 in the age histogram.
- Dropping `Cabin` removed potentially useful deck-location information.
- Dataset covers only the Kaggle Titanic training split — findings may
  not generalize perfectly to unseen data.

---

## Next Steps

- Build a predictive survival model (logistic regression, random forest)
- Engineer additional features (fare-per-person, title extracted from name)
- Apply the same workflow to the Kaggle test set for validation

---

## Dataset Source

Titanic passenger data, originally from the
[Kaggle Titanic competition](https://www.kaggle.com/c/titanic)
and distributed with the `seaborn` library.

