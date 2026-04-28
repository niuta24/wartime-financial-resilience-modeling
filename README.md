# Modeling Financial Resilience in Ukraine's Crop Production Sector
### A Data-Driven Approach under Wartime Conditions

**Bachelor's Thesis** | Ukrainian Catholic University, 2026
**Author:** Anna Syvkova
**Supervisor:** PhD Roman Kornyliuk
**Program:** 124 System Analysis


## Overview

This repository contains the full analytical pipeline for a bachelor's
thesis examining financial distress among Ukrainian crop production
enterprises (NACE 01.11--01.64) during Russia's full-scale invasion
of 2022--2024.

The study asks which enterprises survived the 2022 wartime shock,
which failed, and through what mechanisms --- in order to build an
evidence base for anticipating and mitigating similar shocks in the
future. Using longitudinal registry data on 25,621 legally active
firms observed over 2018--2024, it documents the structural
transformation of the sector and identifies two distinct distress
mechanisms: geographic, where firms in conflict-affected regions
failed through physical destruction regardless of their pre-war
financial health, and financial, where fragile firms in safe regions
collapsed under economic pressure despite being geographically
protected.

These two populations cancel out in aggregate financial comparisons
--- the compositional effect --- rendering classical financial distress
models near-useless in conflict settings even when financial
characteristics are strong predictors within each geographic subgroup.
Geographic augmentation via ACLED conflict-intensity data raises model
AUC from 0.639 (logistic regression, financial only) to 0.900
(gradient boosting, financial + geographic), with conflict intensity
ranking as the dominant predictor by a wide margin (GB importance:
0.425, vs ROA: 0.172).

Among active survivors, 1,153 firms (23.8%) are classified as weak
--- geographically fortunate but structurally fragile, with ROA of
0.023, debt-to-assets of 0.647, and cash-to-assets of 0.008 by 2024,
showing no meaningful recovery across any dimension. They represent
a deferred insolvency risk that wartime support programmes currently
mask.

---

## Repository Structure

```
├── crop_sector_distress_analysis.ipynb               # Main analytical notebook
├── acled_ua_events_2018-2025.xlsx                    # ACLED conflict events by oblast
├── youcontrol_ukraine_crop_financials_2018_2025.xlsx  # Firm-level financial data*
├── geoBoundaries-UKR-ADM1_simplified.geojson         # Ukraine oblast boundaries
├── outputs/                                           # Generated figures (PNG)
├── requirements.txt                                   # Python dependencies
├── LICENSE
└── README.md
```

\* The YouControl dataset is proprietary and cannot be shared publicly.
See **Data Access** below.

---

## Data Sources

| Dataset | Source | Period | Access |
|---------|--------|--------|--------|
| Firm-level financials | YouControl Market (YC.Market); aggregates USR and State Tax Service data | 2018--2024 | Commercial license |
| Conflict events | [ACLED](https://acleddata.com) | 2018--2024 | Free (registration required) |
| Oblast boundaries | [geoBoundaries](https://www.geoboundaries.org) | --- | Open |
| NBU exchange rates | [National Bank of Ukraine](https://bank.gov.ua) | 2018--2024 | Open |

The primary dataset was obtained under a commercial license from
[YouControl Market](https://youcontrol.com.ua/en/) and cannot be
redistributed. Researchers wishing to replicate this study should
obtain access directly from YouControl or contact the author. The
ACLED dataset is freely available after registration at
[acleddata.com](https://acleddata.com/data-export-tool/).

---

## Setup

```bash
git clone https://github.com/niuta24/wartime-financial-resilience-modeling.git
cd wartime-financial-resilience-modeling
pip install -r requirements.txt
jupyter notebook crop_sector_distress_analysis.ipynb
```

**Python version:** 3.10+

---

## Notebook Structure

| Section | Content |
|---------|---------|
| 1. Data Loading & Cleaning | Column reduction pipeline, removal of pre-war closures; final sample 25,621 firms × 78 columns |
| 2. Exploratory Data Analysis | Reporting group segmentation, geographic concentration of reporting silence, Dark Forest analysis |
| 3. Market Transformation 2018--2024 | Revenue geography (oblast maps), wartime shock and reporting paradox, market structure and concentration, financial ratio dynamics |
| 4. Target Variable Definition | Six-rule wartime distress classification, healthy/weak segmentation, estimation sample construction |
| 5. Feature Engineering | Pre-war financial ratios, ACLED conflict-intensity features, correlation screening, train/val/test split (70/15/15) |
| 6. Modeling | Classical benchmarks (Altman, Ohlson), financial-only and geographic-augmented specifications, stratified frontline/non-frontline analysis, coefficient inference |
| 7. Additional Analysis | Regional distress concentration, cash liquidity threshold analysis, size × geography heterogeneity |
| 8. Sensitivity Analysis and Weak Segment | Alternative target definition, geographic distribution of weak survivors, post-war financial dynamics by segment |

---

## Key Results

| Model | Features | AUC |
|-------|----------|-----|
| Altman Z'-score | Financial only | 0.514 |
| Ohlson O-score | Financial only | 0.514 |
| Logistic Regression | Financial only | 0.639 |
| Logistic Regression | ACLED only | 0.698 |
| Logistic Regression | Financial + Geo | 0.749 |
| Random Forest | Financial + Geo | 0.864 |
| **Gradient Boosting** | **Financial + Geo** | **0.900** |

Primary model for predictive performance: **Gradient Boosting
Financial + Geo** (AUC = 0.900). Primary model for coefficient
inference: **Logistic Regression Financial + Geo** (AUC = 0.749,
bootstrap 95% CI). The high GB AUC partly reflects structural
correlation between the geographic feature and the reporting-silence
distress signal; the LR AUC of 0.749 is the more conservative
benchmark.

Among non-frontline firms, financial-only logistic regression
achieves AUC = 0.750 --- confirming that traditional credit screening
retains validity where geographic exposure is low. The gap relative
to frontline firms (AUC = 0.558) directly quantifies the
compositional effect (ΔAUC = 0.192).

---

## License

Code: [MIT License](LICENSE)
Data: see Data Access above.