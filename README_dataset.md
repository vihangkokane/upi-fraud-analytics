# UPI Synthetic Transaction Dataset — Methodology & Availability

## Overview

The original project analysis was designed around a synthetic file named `upi_transactions.csv`, described as containing **202,490 synthetic UPI-style transactions** spanning **January 1 to December 31, 2025**.

The documented methodology says the data was generated using Python libraries including NumPy, Pandas, and Faker. This is synthetic data, not real transaction-level information from NPCI, a bank, a merchant, or an individual customer.

**Availability note:** The full `upi_transactions.csv` and the original dataset-generation script are not present in this repository snapshot. Only `upi_transactions_sample500.csv` (500 rows), `fraud_ground_truth.csv` (202,490 rows), and `fraud_flags_export.csv` (202,490 rows) are included. The full dataset cannot be recreated exactly from the available files.

## Documented population design

The original methodology describes:

- 18,000 synthetic customers, with simulated home location, home bank, baseline average ticket size, and activity weight.
- 2,200 synthetic merchants across Grocery, Food Delivery, Fuel, E-commerce, Utility Bills, Pharmacy, Travel, and Entertainment.
- Approximately 16 states and 40 cities, using directional weights intended to create geographic variation.
- Repeated customers and merchants across transactions to support RFM segmentation and customer-history analysis.

These are design details from the original project documentation; they should not be mistaken for observed facts about real UPI users or merchants.

## Documented seasonality assumptions

The original methodology describes simulated transaction-volume multipliers for:

- Weekdays and weekends.
- Salary-period dates near the start and end of each month.
- Festival and sale windows.
- Hourly patterns, including lower overnight activity and higher evening activity.

The exact source generator is unavailable in this repository, so these assumptions cannot currently be rerun or independently verified.

## Documented payment-failure assumptions

The original documentation describes hand-assigned bank reliability scores, with simulated weaker performance for Yes Bank and Canara Bank and an additional simulated August degradation. It also describes slightly higher failure probability during selected peak hours and weighted failure reasons.

These are synthetic design assumptions, not measured bank performance or allegations about any real financial institution.

## Documented fraud injection

The original methodology describes 2.56% of transactions (5,178 rows) as deliberately injected fraud-pattern examples, with labels stored separately in `fraud_ground_truth.csv`.

| Pattern | Documented description | Documented count |
|---|---|---:|
| `velocity_abuse` | Multiple transactions from the same VPA within a short time window | 1,847 |
| `amount_spike` | Transaction amount far above the customer's simulated historical average | 1,588 |
| `odd_hour_anomaly` | Transaction at an unusual overnight hour for the simulated customer | 1,100 |
| `probing` | Repeated small failed attempts followed by a successful attempt | 643 |

The ground-truth file is intended for evaluation only, not as a model input feature. Because the original transaction file is missing, the correspondence between all labels, transactions, and previously exported flags cannot be independently rechecked using this package alone.

## Known limitations

- Fraud patterns are synthetic and have deliberately clean signatures; real fraud is noisier and adversarial.
- Bank and merchant reliability values are hand-assigned simulation parameters, not fitted to real incident data.
- The documented data does not include all real-world risk signals such as device fingerprint, IP address, or geolocation drift.
- Geographic weights are directional estimates, not official NPCI statistics.
- Transaction amount distributions are simulated and may not capture the full complexity of real spending behaviour.
- The original generator and full source CSV are unavailable here, so the original full dataset and analysis outputs are not fully reproducible from this repository snapshot.

## Files in this repository

- `upi_transactions_sample500.csv` — 500-row transaction sample.
- `fraud_ground_truth.csv` — synthetic transaction labels for evaluation.
- `fraud_flags_export.csv` — previously exported fraud-flag results.
- `UPI_Fraud_EDA_Analysis.ipynb` — analysis notebook; expects the missing `upi_transactions.csv`.

## Reproduction status

The original full dataset-generation process cannot be reproduced exactly from this repository because its generator script and full source CSV are not included. Do not infer or fabricate missing transaction records from the labels or exported flags. To restore end-to-end reproducibility, add the original full synthetic transaction data or create and clearly document a new generator, then rerun the SQL, notebook, dashboard refresh, and business report so that all outputs correspond to the same dataset.
