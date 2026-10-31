# UPI Fraud Analytics Platform

**Project owner / maintainer:** Vihang Kokane  
**GitHub:** [@vihangkokane](https://github.com/vihangkokane)  
**Domain:** FinTech | Transaction Analytics | Fraud Risk Analysis  
**Tools:** SQL, Python, Pandas, Jupyter Notebook, Power BI

## Overview

An end-to-end analytics project exploring synthetic UPI-style payment transactions, payment failures, merchant performance, customer segments, and suspicious transaction patterns.

The project combines SQL-based business analysis, Python exploratory data analysis and an explainable rule-based fraud-flagging approach, with a Power BI dashboard and a stakeholder-oriented insights summary.

> **Data disclaimer:** The data described by this project is synthetic. It does not represent actual NPCI, bank, merchant, or customer transaction records. Findings and model metrics must not be interpreted as real-world UPI fraud rates or bank performance.

## Business questions

- How do transaction volumes and values change over time?
- Which banks, cities, and transaction categories have higher payment failure rates?
- Which merchants and categories contribute the most successful transaction value?
- How can customers be segmented using recency, frequency, and monetary value?
- Which transactions match the project's suspicious-activity rules?
- What are the trade-offs between identifying suspicious activity and generating false positives?

## Repository contents

| File | Purpose |
|---|---|
| `01_volume_trends.sql` | Transaction volume, value, monthly movement, hourly and weekday patterns |
| `02_failure_analysis.sql` | Failure rates by bank, month, city, reason, and merchant category |
| `03_merchant_performance.sql` | Merchant success rates, revenue, ticket size, and rankings |
| `04_geographic_patterns.sql` | State/city summaries and geographic transaction mix |
| `05_customer_rfm.sql` | Customer profiles, RFM scores, and customer segments |
| `UPI_Fraud_EDA_Analysis.ipynb` | Python EDA, rule-based fraud flags, validation, and impact analysis |
| `fraud_flags_export.csv` | Exported per-transaction fraud-flag results |
| `fraud_ground_truth.csv` | Synthetic labels used to evaluate the rule-based flags |
| `upi_transactions_sample500.csv` | 500-row sample of the synthetic transaction data |
| `dashboard.pbix` | Power BI dashboard |
| `UPI_Insights_Pastel_Theme.json` | Power BI theme |
| `dashboard_background.png` | Dashboard background asset |
| `Business_Insights_Summary.docx` | Stakeholder insights and recommendations |
| `README_dataset.md` | Dataset design, assumptions, and limitations |

## Analytical workflow

1. **SQL transaction analysis** — volume, failures, merchants, geography, and customer RFM.
2. **Python exploratory analysis** — transaction distributions, time patterns, bank performance, and merchant categories.
3. **Rule-based suspicious-activity analysis** — velocity, amount-spike, odd-hour, and probing patterns.
4. **Evaluation** — compare flags with synthetic ground-truth labels using precision and recall.
5. **Business intelligence** — explore the Power BI dashboard and communicate findings and recommendations.

## Dataset availability — read before running

The original project documentation describes a synthetic dataset named `upi_transactions.csv` containing 202,490 transactions. **That full source CSV is not included in this repository snapshot.** The uploaded project package contains:

- `upi_transactions_sample500.csv` — a 500-row sample;
- `fraud_ground_truth.csv` — 202,490 synthetic transaction labels;
- `fraud_flags_export.csv` — 202,490 rows of previously exported fraud-flag results.

The Python notebook expects `upi_transactions.csv` and therefore cannot currently be rerun end-to-end from this repository alone. The 500-row sample is not a substitute for the full source file. The full dataset-generation script is also not included, so the original full dataset cannot be recreated exactly from the files in this repository.

The existing dashboard and business-insights document are retained as project artefacts from the prior analysis. Their reported figures should be treated as previously generated outputs, not as results that a new user can independently reproduce from the currently included source data. Do not claim that the full workflow is reproducible until the full transaction source data or a replacement generation pipeline has been added and the outputs have been revalidated.

## SQL execution notes

The SQL scripts were prepared for MySQL 8.0. The original workflow expects the full transaction table to be loaded into a database named `upi_insights`. Because the full `upi_transactions.csv` is not included, the scripts cannot be validated end-to-end against the complete dataset from this package alone.

## Python notebook notes

Open `UPI_Fraud_EDA_Analysis.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab. Its initial data-loading cell expects `upi_transactions.csv`, which is currently unavailable in this repository. The included 500-row sample may be useful for inspecting the schema, but it will not reproduce the original full-data outputs.

## Power BI dashboard notes

Open `dashboard.pbix` in Power BI Desktop. If Power BI prompts for data-source paths, the original full source dataset is not present in this package. The dashboard is included for inspection, but refreshing all visuals may require the original source data and/or the original Power BI data model.

## Interpretation and limitations

- Fraud patterns in the documented methodology are synthetic and deliberately injected. Performance metrics on these labels do not establish real-world fraud-detection performance.
- Rule-based flags are investigation signals, not proof that a transaction is fraudulent.
- Bank and merchant reliability settings are simulation assumptions, not official bank statistics.
- Geographic weights are directional simulation assumptions, not official NPCI figures.
- The documented odd-hour rule has relatively low standalone precision, illustrating the false-positive trade-off.
- The absence of the full transaction CSV limits independent reproduction and validation of the included dashboard and report.

## Ownership and maintenance

This repository is maintained by **Vihang Kokane**. The project is being documented and maintained on GitHub as part of a data analytics portfolio.
