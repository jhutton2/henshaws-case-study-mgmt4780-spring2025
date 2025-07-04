# Spring 2025 | MGT 4380 HR Analytics
Below includes detailed methods, code logic, decisions, transformations, and data issues encountered and resolved.

# 1. Dataset Overview

Codebook summary can be found [here](Henshaws_Codebook_Summary.xlsx).
- Original Source: SPSS files with four tables — Employee Survey, Financials, Labor Risk, and Customer Data.
- Merged in: SPSS, then exported to CSV for analysis in Python and visualization in Power BI.
- Grain: One row = one store
- Critical Variables: EngagementScore, YTDPROFIT, SUBTOTALSALES, NetTurnover, CSAT2019, CustComplaints
# 2. Cleaning Process
All fixes are documented in the [change-log](Henshaw_Changelog.xlsx).
Python code for cleaning can be found [here](henshaw's.py).

## 2.1 Data Understanding
- Grain confirmed: Store-level aggregation
- Measures: Engagement score, profit, sales, turnover, etc.
- Dimensions: District, Store Number
- Critical Variables Confirmed: EngagementScore, YTDPROFIT, SUBTOTALSALES, NetTurnover, CSAT2019, CustComplaints
## 2.2 Solvable Issues
- Missing Thresholds:
  - Dropped stores with N_EEs < 5
  - Removed stores missing critical financial or customer data
- Outliers: Used z-scores; flagged stores with |z| > 3 on financials and engagement
- Field Formatting: Converted object columns to numeric
## 2.3 Unsolvable Issues
- Minimal impact cases (<10%) were dropped
## 2.4 Augmentations
- EngagementScore: Created from survey subcomponents or used provided EngagementStoreAverage
- Final Include Flag: Filtered data where:
    - N_EEs ≥ 5
    - Not missing critical variables
    - Not flagged as outliers
- DAX Augmentations are in
# 3 Analysis Methods
3.1 Correlations
- Test Used: Pearson correlation
- Subgroup: Only filtered data (include_flag == 1)
- IVs/DVs:
    - Engagement vs Profit → r = 0.292, p = 0.001
    - Engagement vs Sales → r = 0.231, p = 0.010
    - Engagement vs Turnover → r = -0.147, p = 0.104
    - Turnover vs CSAT → r = -0.38, p = 0.00008
    - Turnover vs Complaints → r = 0.30, p = 0.0012
3.2 Regression (Profit and Engagement)
  - R² = 0.071
  - Coefficient = 35.63
  -  p-value = 0.002

# 4. Power BI Dashboard Logic
DAX logic can be found [here](henshaws-dax-measures.md).
Metrics Created
  - District with Lowest Engagement
  - District with Lowest Profit
  - District with Both (Combo Priority)
  - Low Engagement Store Count (<50%)
# 5. Caveats and Assumptions 
- Survey data may be non-representative in stores with few respondents
- No time component means causal inference is limited
- Multivariate Analysis (e.g., controlling for district) could deepen insights but was out of scope
- Turnover is annualized, exact timing of exits is unknown
    
