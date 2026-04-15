# Modeling of Financial Resilience in Ukraine's Crop Production Sector: A Data-Driven Approach under Wartime Conditions

This repository contains the analytical framework and implementation code for a bachelor thesis. The study pursues two complementary aims: conducting a comprehensive market dynamics analysis of Ukraine's crop production sector (2018–2024) and developing a retrospective classification framework for financial distress during the acute phase of the 2022–2023 crisis.

## Overview and Market Research
Unlike traditional financial studies, this research employs distress prediction as a lens to examine broader structural transformations in the sector. Key market research findings include:
* **Structural Transformation**: The sector underwent a 63% collapse in median revenue in 2022, followed by a structural shift in geographic distribution and market concentration.
* **The Wartime Paradox**: A significant increase in reporting firms (from 5,022 to 10,264) was documented, driven by the formalization of 6,308 shadow economy entities seeking state support.
* **Market Concentration**: The revenue share controlled by the top 10% of firms surged from 60.6% to 72.4%, indicating reduced competition and selective exit.

## Sample Construction and Methodology
The study uses a rigorous "funnel" approach to define the final analytical sample:
1. **Initial Sample**: 34,944 registered crop production entities (NACE 01.11-01.64).
2. **Active Firms**: 25,621 entities legally active at the onset of the full-scale invasion (9,323 pre-war closures removed).
3. **Base Analytical Sample**: 6,237 firms that had submitted financial reports during the pre-war period (2018–2021).
4. **Final Model Sample**: 5,350 firms remaining after applying the six-rule wartime distress classification and excluding 887 ambiguous cases (firms with active status but no 2021 reporting baseline).

## Key Components
* **Backtesting Framework**: A point-in-time design simulating the information available to analysts in early 2022.
* **Feature Engineering**: Integration of 16 features across financial ratios (profitability, liquidity, leverage) and geospatial conflict-intensity variables from the ACLED dataset.
* **Predictive Performance**: Logistic Regression and Decision Tree models achieve an AUC improvement of +0.235 when augmented with geographic risk factors, reaching a test AUC of 0.771.
* **Dual Mechanism Identification**: Classification of distress into geographic (frontline-driven) and financial (fragility-driven) failure modes.

## Repository Structure
* `crop_sector_distress_analysis.ipynb`: End-to-end pipeline (Data cleaning, EDA, Market dynamics, Modeling).
* `outputs/`: Visualization of results, including market structure evolution, factor significance, and model comparison.
* `requirements.txt`: Environment configuration for reproducibility.
* `geoBoundaries-UKR-ADM1_simplified.geojson`: Data for geospatial mapping.

## Data Access
The primary firm-level dataset is proprietary (sourced from YouControl Market) and is excluded from this repository. Detailed feature definitions and summary statistics are provided within the notebook.

---
**Author:** Anna SYVKOVA  
**Supervisor:** PhD Roman KORNYLIUK  
**Institution:** Ukrainian Catholic University, Faculty of Applied Sciences (2026)
