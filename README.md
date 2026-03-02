# Measuring How Organizational Volatility Propagates

## Overview

Organizations operate in environments characterized by uncertainty: shifting demand, changing costs, and unpredictable macroeconomic conditions. Firms often attempt to stabilize financial outcomes such as earnings and margins. However, if variability is reduced in one part of a system, it may appear elsewhere.

This project investigates a specific question:

> **When companies face uncertainty, where does the volatility go?**

More specifically:

> How does organizational uncertainty propagate into household financial behavior?<br>
> Are we doing the best we can, or are there opportunities for improvement?

The goal of this project is not to make moral claims about corporations, but to operationalize a question about risk distribution in the modern landscape.

---

## Research Approach

The project models uncertainty as a **distribution problem** rather than a single metric.

Three systems are measured:

### 1. Organizational Labor Volatility
- Technology sector layoffs in California  
- Sources: Layoffs.fyi and California WARN notices

### 2. Firm Financial Stability
- Quarterly financial variance (revenue, earnings)  
- Public company filings and financial data

### 3. Household Financial Stress
- Credit delinquency and borrowing behavior  
- New York Fed Household Debt and Credit data

By aligning these datasets temporally, the analysis tests whether labor instability increases during periods of elevated organizational uncertainty and whether household financial indicators shift afterward.

---

## Key Concept: Labor Shock Absorber Index (LSAI)

The project introduces a metric:

**Labor Shock Absorber Index (LSAI)**

LSAI compares labor volatility to financial volatility to evaluate whether variability is concentrated in employment rather than earnings.

The intent is descriptive, not causal: the analysis examines patterns of alignment, not proof of intent.

---

## Data Pipeline

1. Download layoff event data (Layoffs.fyi, California WARN)
2. Clean and standardize dates to quarterly periods
3. Aggregate layoffs by quarter
4. Align with financial and household datasets
5. Visualize lagged relationships

All data processing scripts are located in `/scripts`.

---

## Why This Matters

Many discussions of layoffs, automation, and economic anxiety are framed as cultural or managerial issues. This project treats them as **system behaviors**.

If organizations reduce uncertainty internally while increasing it externally, at what point does the external uncertainty come back around to the organization again?

Understanding this distribution may inform:

- consumer demand
- workforce planning
- risk management
- sustainability reporting
- the future role of analytics in decision-making

---

## Status

**Current phase:** data acquisition and initial labor volatility index construction.

**Upcoming:**
- household credit alignment
- spending behavior analysis
- narrative interpretation

---

## Author
Vesper Annstas<br>
https://www.linkedin.com/in/vesperannstas/
This project originated as an attempt to translate an ambiguous question into a measurable analytical framework. It may or may not produce actionable insights.