# henshaws-case-study-mgmt4780-spring2025
HR analytics case study from MGMT 4780 (Spring 2025) analyzing the impact of employee engagement and turnover on profit, sales, and customer experience for a gas station retail chain.
# Background Overview
Henshaw's is a fictional convenience store and gas station chain operating in the Southeastern United States. This project was conducted in the context of an HR analytics consulting simulation to explore the relationship between employee culture, engagement, turnover, and store-level performance. As part of the analysis, data was collected and merged from multiple business domains, including labor risk assessments, financial performance, employee surveys, and customer satisfaction. This project was conducted as part of an academic HR analytics consulting simulation at Georgia State University.

* Python-based data cleaning and outlier handling scripts can be found [here](docs/henshaw's.py).
* The Power BI dashboard can be downloaded [here](docs/Henshaw's.pbix).
* A full technical breakdown can be found [here](docs/technical-notes.md).

# Data Structure Overview 
The dataset included four key files:
* Labor Risk File: store-level risk scores and cheer (loyalty) scores
* Finance File: profit, sales, and turnover metrics
* Employee Survey File: engagement, satisfaction, teamwork, leadership scores
* Customer Data File: CSAT and customer complaint volumes
Each file was merged using the store number as the unique identifier. After preprocessing, outlier filtering, and validity checks, a clean dataset of 136 stores was retained for analysis

# Executive Summary
This analysis uncovered several key insights about how culture and people dynamics affect Henshaw's store-level outcomes:
* Engagement is positively associated with profitability (r = 0.29, p = 0.001) — more engaged employees tend to work in stores with better bottom-line performance.
* Engagement did not significantly predict turnover (r = –0.15, p = 0.104) — suggesting turnover may be driven by factors outside of engagement alone.
* Turnover negatively impacts customer satisfaction (r = –0.38, p < 0.001) and increases customer complaints (r = 0.30, p = 0.0012), making it a visible business risk.
* Districts with both low engagement and low profit were flagged as top-priority areas for cultural and operational intervention.
These findings support the need for leadership to view HR and engagement initiatives not as “soft investments,” but as drivers of store efficiency, customer loyalty, and financial stability.
![Power BI screenshot showing KPIs by district](docs/dashboard_overview.png)


# Insights Deep Dive
| Metric                  | Value                | Interpretation                                                       |
| ----------------------- | -------------------- | ------------------------------------------------------------------------ |
| Engagement vs. Profit   | r = 0.29, p = 0.001  | Moderately positive — engagement appears linked to financial performance |
| Engagement vs. Turnover | r = –0.15, p = 0.10  | Weak, not statistically significant                                      |
| Turnover vs. CSAT       | r = –0.38, p < 0.001 | Stronger — turnover likely affects customer satisfaction                 |

### Engagement & Profit
* A linear regression showed that a 1-point increase in average engagement score predicted a 35.6% increase in YTD profit.
* This relationship held even when controlling for outliers and filtering stores with fewer than 5 employees.
* Engagement did not significantly correlate with total sales, suggesting its impact lies more in cost control, service quality, or efficiency.

### Engagement & Turnover
* While we expected higher engagement to result in lower turnover, the observed relationship was weak and not statistically significant.
* This implies turnover may be influenced by other factors like leadership, pay structure, or labor market dynamics.

### Turnover & Customer Experience
* High turnover stores had lower CSAT and higher complaint volume, confirming turnover as a frontline customer issue.
* Even in the absence of strong engagement-to-turnover links, turnover still deserves attention due to its external business consequences.

### Risk District Identification
* Using DAX-based KPIs, the Power BI dashboard flagged:
    * Districts with lowest average engagement
    * Districts with lowest profit
    * Stores below a 60% engagement threshold
    * Bottom 5 districts based on combined engagement + profit risk score

# Recommendations
* Focus engagement and leadership development efforts in the bottom 5 districts flagged for low engagement and profit.
* Reevaluate current turnover strategies: since engagement alone doesn’t predict retention, additional drivers (manager stability, compensation, etc.) should be assessed.
* Incorporate turnover impact into customer satisfaction KPIs — view turnover as a customer-facing risk.
* Use cultural metrics (cheer, engagement) in store performance reviews alongside financial metrics.

# Caveats and Assumptions
* Some data fields had missing or blank values, particularly in profit and survey scores; rows were filtered based on an inclusion flag with minimum employee count and data completeness.
* Engagement data was self-reported, which may introduce subjectivity or non-response bias.
* No time-series data was available, limiting trend or lag-based analysis.
* The relationship between variables may be influenced by unobserved confounders (e.g., manager experience, store size) not included in the dataset.
