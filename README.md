# Modeling Financial Resilience in Ukraine's Crop Production Sector
### A Data-Driven Approach under Wartime Conditions

**Bachelor's Thesis** | Ukrainian Catholic University, 2026  
**Author:** Anna Syvkova  
**Supervisor:** PhD Roman Kornyliuk  
**Program:** 124 System Analysis

---

## Overview

This repository contains the full analytical pipeline for a study of financial
distress among Ukrainian crop production enterprises (NACE 01.11–01.64) during
the full-scale war of 2022–2024.

The central finding: location determined survival more than any balance-sheet ratio.
A single binary indicator — whether a firm operated in a frontline oblast —
outperforms twelve pre-war financial ratios in predicting wartime distress.
Financial models work in safe regions (AUC = 0.749) but collapse to near-random
on frontline firms (AUC = 0.552), confirming two structurally distinct distress
mechanisms: geographic destruction and financial fragility.

---

## Repository Structure

```
├── crop_sector_distress_analysis.ipynb   # Main analytical notebook (6 sections)
├── acled_ua_events_2018-2025.xlsx        # ACLED conflict events by oblast
├── youcontrol_ukraine_crop_financials_2018_2025.xlsx  # Firm-level financial data*
├── geoBoundaries-UKR-ADM1_simplified.geojson          # Ukraine oblast boundaries
├── outputs/                              # Generated figures (PNG)
├── requirements.txt                      # Python dependencies
├── LICENSE
└── README.md
```

\*The YouControl dataset is proprietary and cannot be shared publicly.
See **Data Access** below.

---

## Data Sources

| Dataset | Source | Period | Access |
|---------|--------|--------|--------|
| Firm-level financials | YouControl Market | 2018–2024 | Commercial license |
| Conflict events | [ACLED](https://acleddata.com) | 2018–2024 | Free (registration required) |
| Oblast boundaries | [geoBoundaries](https://www.geoboundaries.org) | — | Open |
| NBU exchange rates | [National Bank of Ukraine](https://bank.gov.ua) | 2018–2024 | Open |

### Data Access

The primary dataset (`youcontrol_ukraine_crop_financials_2018_2025.xlsx`) was
obtained under a commercial license from
[YouControl Market](https://youcontrol.com.ua/en/) and cannot be redistributed.
Researchers wishing to replicate this study should obtain access directly from
YouControl or contact the author.

The ACLED dataset is freely available after registration at
[acleddata.com](https://acleddata.com/data-export-tool/).

---

## Setup

```bash
# Clone the repository
git clone https://github.com/niuta24/wartime-financial-resilience-modeling.git
cd wartime-financial-resilience-modeling

# Install dependencies
pip install -r requirements.txt

# Launch the notebook
jupyter notebook crop_sector_distress_analysis.ipynb
```

**Python version:** 3.10+

---

## Notebook Structure

| Section | Content |
|---------|---------|
| 0. Setup | Imports, visualization styles, constants, helper functions |
| 1. Data Loading & Cleaning | 9-step cleaning pipeline, final sample of 25,621 firms |
| 2. Exploratory Data Analysis | Reporting group segmentation, geographic distribution |
| 3. Market Research 2018–2024 | Revenue geography, wartime shock, market structure |
| 4. Target Variable Definition | Six-rule distress classification, geographic validation |
| 5. Feature Engineering | Financial ratios, ACLED conflict features, train/val/test split |
| 6. Modeling | Benchmarks, LR, Random Forest, Gradient Boosting, post-hoc validation |

---

## Key Results

| Model | Features | AUC |
|-------|----------|-----|
| Altman Z'-score | Financial only | 0.514 |
| Ohlson O-score | Financial only | 0.522 |
| Logistic Regression | Financial only | 0.648 |
| Logistic Regression | Frontline only | 0.674 |
| **Logistic Regression** | **Financial + Geo** | **0.781** |
| Random Forest | Financial + Geo | 0.867 |
| Gradient Boosting | Financial + Geo | 0.894 |

Primary model: **Logistic Regression Financial + Geo** — selected for
interpretability. Produces standardised coefficients and p-values identifying
which features determine wartime survival.

---

## License

Code: [MIT License](LICENSE)  
Data: see Data Access above.