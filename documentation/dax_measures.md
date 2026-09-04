# DAX Measures — Cabinet Office Spend Analysis

## 1. Spend Measures

**Total Spend**  
```
Total Spend = SUM(Finance_Expenditure[Amount])

**Average Transaction Value**  
Avg Transaction Value = AVERAGE(Finance_Expenditure[Amount])
```

## 2. Date Table (Fiscal Year: April → March)

**Date Table (Calculated Table)**  
Date_Table = 
ADDCOLUMNS(
    CALENDAR(DATE(2025,4,1), DATE(2026,3,31)),
    "Year", YEAR([Date]),
    "Month", MONTH([Date]),
    "MonthName", FORMAT([Date], "MMMM"),
    "FinancialMonth", IF(MONTH([Date])>=4, MONTH([Date])-3, MONTH([Date])+9),
    "FinancialYear", IF(
        MONTH([Date])>=4,
        YEAR([Date]) & "/" & YEAR([Date])+1,
        YEAR([Date])-1 & "/" & YEAR([Date])
    ),
    "Quarter", "Q" &
        ROUNDUP(
            IF(MONTH([Date])>=4, MONTH([Date])-3, MONTH([Date])+9) / 3,
            0
        )
)


## 3. Month-on-Month Change

**MoM Change**  
MoM Change = 
IF(
    ISBLANK([Prior Month Spend]),
    BLANK(),
    [Total Spend] - [Prior Month Spend]
)


## 4. Invoice Size Segmentation

**Invoice Size Bucket**  
Invoice Size Bucket = 
SWITCH(
    TRUE(),
    'Finance_Expenditure'[Amount] <= 100000, "£25k - £100K",
    'Finance_Expenditure'[Amount] <= 500000, "£100K - £500K",
    'Finance_Expenditure'[Amount] <= 1000000, "£500K - £1M",
    "Over £1M"
)
