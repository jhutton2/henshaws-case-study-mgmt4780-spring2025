# Spring 2025 | MGT 4380 HR Analytics
Below includes detailed methods, code logic, decisions, transformations, and data issues encountered and resolved.

# Dataset Overview
- Original Source: SPSS files with four tables — Employee Survey, Financials, Labor Risk, and Customer Data.
- Merged in: SPSS, then exported to CSV for analysis in Python and visualization in Power BI.
- Grain: One row = one store
- Critical Variables: EngagementScore, YTDPROFIT, SUBTOTALSALES, NetTurnover, CSAT2019, CustComplaints
# Cleaning Process
All fixes are documented 
Data Understanding
- Grain confirmed: Store-level aggregation
- Measures: Engagement score, profit, sales, turnover, etc.
- Dimensions: District, Store Number
- Critical Variables Confirmed: EngagementScore, YTDPROFIT, SUBTOTALSALES, NetTurnover, CSAT2019, CustComplaints
Solvable Issues
- Missing Thresholds:
  - Dropped stores with N_EEs < 5
  - Removed stores missing critical financial or customer data
- Outliers: Used z-scores; flagged stores with |z| > 3 on financials and engagement
- Field Formatting: Converted object columns to numeric
Unsolvable Issues
- Minimal impact cases (<10%) were dropped
Augmentations
- EngagementScore: Created from survey subcomponents or used provided EngagementStoreAverage
- Final Include Flag: Filtered data where:
    - N_EEs ≥ 5
    - Not missing critical variables
    - Not flagged as outliers
