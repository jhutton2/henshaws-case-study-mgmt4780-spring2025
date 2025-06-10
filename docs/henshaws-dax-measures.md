
# DAX Measures – Henshaw's Dashboard

This file documents the key DAX measures used in the Power BI dashboard to calculate business-critical metrics related to employee engagement, store performance, and operational risk.

---

## District-Level KPIs

### Lowest Engagement District
```DAX
Lowest Engagement District = 
VAR SummaryTable =
    SUMMARIZE(
        'henshaws_cleaned_dataset', 
        'henshaws_cleaned_dataset'[District], 
        "AvgEngagement", AVERAGE('henshaws_cleaned_dataset'[EngagementScore])
    )
VAR LowestRegionRow = TOPN(1, SummaryTable, [AvgEngagement], ASC)
RETURN
    SELECTCOLUMNS(LowestRegionRow, "District", 'henshaws_cleaned_dataset'[District])
```
### Lowest Profit District
```DAX
LowestProfitDistrict = 
VAR SummaryTable =
    SUMMARIZE(
        'henshaws_cleaned_dataset', 
        'henshaws_cleaned_dataset'[District], 
        "AvgProfit", AVERAGE('henshaws_cleaned_dataset'[YTDPROFIT])
    )
VAR LowestDistrictRow = TOPN(1, SummaryTable, [AvgProfit], ASC)
RETURN
    SELECTCOLUMNS(LowestDistrictRow, "District", [District])
```

---

## Store-Level Risk Indicators

### Low Engagement Store Count (< 50%)
```DAX
# of Low Engagement Stores = 
CALCULATE(
    COUNTROWS('henshaws_cleaned_dataset'),
    'henshaws_cleaned_dataset'[EngagementScore] < .508
)
```

---

## Combo Metric: Engagement + Profit

### DistrictComboSummary
```DAX
DistrictComboSummary = 
ADDCOLUMNS(
    SUMMARIZE('henshaws_cleaned_dataset', 'henshaws_cleaned_dataset'[District]),
    "AvgEngagement", CALCULATE(AVERAGE('henshaws_cleaned_dataset'[EngagementScore])),
    "AvgProfit", CALCULATE(AVERAGE('henshaws_cleaned_dataset'[YTDPROFIT])),
    "CombinedScore", 
        CALCULATE(AVERAGE('henshaws_cleaned_dataset'[EngagementScore])) + 
        CALCULATE(AVERAGE('henshaws_cleaned_dataset'[YTDPROFIT]))
)

```

---

## Notes
- All calculations respect filters implied by the `include_flag` logic used during preprocessing
- This file is designed to make metrics transparent and portable across dashboards
