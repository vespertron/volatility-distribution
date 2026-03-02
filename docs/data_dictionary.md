# Data Dictionary

This document describes the datasets constructed and used in the volatility distribution project.

All datasets are aggregated at the quarterly level unless otherwise noted.

---

# 1. layoff_events

Granular layoff event data derived from California WARN Act filings.

Unit of observation: Individual layoff notice.

| Column | Type | Description |
|--------|------|------------|
| company | string | Name of firm filing WARN notice |
| notice_date | date | Date of WARN filing |
| year | integer | Calendar year derived from notice_date |
| quarter | string | Calendar quarter (e.g., 2023Q2) |
| employees_affected | integer | Number of employees impacted by the notice |
| county | string | California county of reported layoff |
| layoff_type | string | Permanent layoff, temporary layoff, closure (if available) |

Notes:
- Only California-based WARN filings are included.
- Small workforce adjustments not subject to WARN may not be captured.

---

# 2. layoffs_by_quarter

Quarterly aggregation of layoff activity.

Unit of observation: Quarter.

| Column | Type | Description |
|--------|------|------------|
| quarter | string | Calendar quarter (e.g., 2023Q2) |
| year | integer | Calendar year |
| quarter_num | integer | Quarter number (1–4) |
| layoffs_total | integer | Total employees affected in the quarter |
| companies_laying_off | integer | Count of distinct firms issuing WARN notices |
| avg_layoff_size | float | Mean employees affected per layoff event |

Derived from:
- Aggregation of `layoff_events`

Purpose:
- Measures organizational labor volatility at quarterly frequency.

---

# 3. company_financials

Quarterly firm-level financial data for selected technology firms.

Unit of observation: Company-quarter.

| Column | Type | Description |
|--------|------|------------|
| company | string | Publicly traded technology firm |
| quarter | string | Calendar quarter |
| revenue | float | Quarterly revenue (USD) |
| eps | float | Earnings per share |
| operating_income | float | Quarterly operating income (USD) |
| operating_margin | float | Operating income divided by revenue |

Derived fields (calculated in analysis phase):

| Column | Type | Description |
|--------|------|------------|
| revenue_volatility | float | Rolling 8-quarter standard deviation of revenue |
| eps_volatility | float | Rolling 8-quarter standard deviation of EPS |
| margin_volatility | float | Rolling 8-quarter standard deviation of operating margin |

Purpose:
- Measures firm-level financial volatility.

---

# 4. household_credit

State-level household financial stress indicators for California.

Source: New York Fed Household Debt and Credit dataset.

Unit of observation: Quarter.

| Column | Type | Description |
|--------|------|------------|
| quarter | string | Calendar quarter |
| credit_card_delinquency_90 | float | Percent of balances 90+ days delinquent |
| new_delinquency_rate | float | Share of accounts transitioning into delinquency |
| revolving_credit_balance | float | Total revolving credit balance (USD) |
| total_debt_balance | float | Total household debt balance (USD) |

Derived field:

| Column | Type | Description |
|--------|------|------------|
| credit_stress_index | float | Composite index constructed using standardized delinquency and revolving balance growth measures |

Purpose:
- Proxy for household financial resilience.

---

# 5. uncertainty_transmission_panel

Merged quarterly dataset combining labor volatility, financial volatility, and household stress indicators.

Unit of observation: Quarter.

| Column | Type | Description |
|--------|------|------------|
| quarter | string | Calendar quarter |
| layoffs_total | integer | Total WARN-reported layoffs |
| companies_laying_off | integer | Number of firms issuing WARN notices |
| revenue_volatility | float | Sector-level revenue volatility |
| eps_volatility | float | Sector-level EPS volatility |
| credit_stress_index | float | Household financial stress measure |
| layoffs_lag1 | integer | Prior quarter layoffs_total |
| credit_stress_lag1 | float | Prior quarter credit_stress_index |

Purpose:
- Enables temporal alignment and lag analysis.

---

# Key Derived Metric

## Labor Shock Absorber Index (LSAI)

LSAI = Labor Volatility ÷ Financial Volatility

Where:

- Labor Volatility = layoffs_total (or standardized measure)
- Financial Volatility = revenue_volatility or eps_volatility

Interpretation:
- LSAI > 1 suggests volatility is more concentrated in employment.
- LSAI < 1 suggests volatility is more concentrated in financial outcomes.

---

# Data Governance Notes

- All data is aggregated and publicly available.
- No individual-level data is used.
- Correlation-based analysis; no causal inference claims are made in the current phase.

---

# Version

Version 1.0 — WARN-based labor volatility model.