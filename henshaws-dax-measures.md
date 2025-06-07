
# DAX Measures – Henshaw's Dashboard

This file documents the key DAX measures used in the Power BI dashboard to calculate business-critical metrics related to employee engagement, store performance, and operational risk.

---

## 🔹 District-Level KPIs

### Lowest Engagement District
```DAX
LowestEngagementDistrict = 
VAR SummaryTable =
    SUMMARIZE(
        'henshaws_cleaned_dataset',
        'henshaws_cleaned_dataset'[District],
        "AvgEngagement", AVERAGE('henshaws_cleaned_dataset'[EngagementStoreAverage])
    )
VAR LowestRegionRow = TOPN(1, SummaryTable, [AvgEngagement], ASC)
RETURN
    SELECTCOLUMNS(LowestRegionRow, "District", [District])
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
VAR LowestRegionRow = TOPN(1, SummaryTable, [AvgProfit], ASC)
RETURN
    SELECTCOLUMNS(LowestRegionRow, "District", [District])
```

---

## 🔹 Store-Level Risk Indicators

### Low Engagement Store Count (< 60%)
```DAX
LowEngagementStoreCount = 
CALCULATE(
    COUNTROWS('henshaws_cleaned_dataset'),
    'henshaws_cleaned_dataset'[EngagementStoreAverage] < 0.60
)
```

---

## 🔹 Combo Metric: Engagement + Profit

### Combo Score
```DAX
ComboScore = 
AVERAGEX(
    VALUES('henshaws_cleaned_dataset'[StoreNumber]),
    (
        'henshaws_cleaned_dataset'[EngagementStoreAverage] + 
        'henshaws_cleaned_dataset'[YTDPROFIT]
    ) / 2
)
```

### Rank Bottom 5 Combo Stores
```DAX
ComboRank = 
RANKX(
    ALL('henshaws_cleaned_dataset'[StoreNumber]),
    [ComboScore],
    ,
    ASC
)
```

---

## 📌 Notes
- All calculations respect filters implied by the `include_flag` logic used during preprocessing
- This file is designed to make metrics transparent and portable across dashboards
