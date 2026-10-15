# DAX Measures — Healthcare Data Warehouse

25 measures across five required DAX families (8 math/statistical, 5 counting, 4 logical/conditional, 4 CALCULATE filter-context, 4 time intelligence).

## Counting
| # | Measure | Logic |
|---|---------|-------|
| 1 | Total Encounters | `COUNTROWS` of the fact table |
| 4 | Distinct Patients | `DISTINCTCOUNT(PatientID)` |
| 11 | Readmitted Encounters | `COUNTROWS` filtered to ReadmissionFlag = 1 |
| 12 | Encounters per Patient | Total Encounters ÷ Distinct Patients |
| 13 | Active Facilities | `DISTINCTCOUNT(FacilityID)` in the fact table |

## Math / statistical
| # | Measure | Logic |
|---|---------|-------|
| 2 | Total Charges | `SUM` of gross billed |
| 3 | Total Cost | `SUM` of delivery cost |
| 5 | Avg Length of Stay | `AVERAGE` stay in days |
| 6 | Median Charge | `MEDIAN` charge (robust to outliers) |
| 7 | Charge Std Dev | `STDEV.P` of charges |
| 8 | Avg Charge per Encounter | Total Charges ÷ encounter count |
| 9 | Contribution Margin | Total Charges − Total Cost |
| 10 | Margin % | Contribution Margin ÷ Total Charges |

## Logical / conditional
| # | Measure | Logic |
|---|---------|-------|
| 14 | Readmission Rate | `DIVIDE(Readmitted, Total Encounters)` (safe zero denominator) |
| 15 | Margin Status | `SWITCH(TRUE())` → Above / On / Below Target |
| 16 | Readmission Alert | `IF` flags groupings above an 18% readmission rate |
| 17 | High Cost Encounters | counts encounters above the 75th-percentile charge ($36,506) |

## CALCULATE (filter-context modification)
| # | Measure | Logic |
|---|---------|-------|
| 18 | Hospital Charges | `CALCULATE` restricted to hospital facilities |
| 19 | Clinic Charges | `CALCULATE` restricted to clinic facilities |
| 20 | % of Total Charges | `CALCULATE` with `ALL` to remove the facility filter |
| 21 | Chronic Readmission Rate | Readmission Rate within a Chronic diagnosis filter |

## Time intelligence
| # | Measure | Logic |
|---|---------|-------|
| 22 | Charges YTD | `TOTALYTD` from the start of the calendar year |
| 23 | Charges PY | `SAMEPERIODLASTYEAR` |
| 24 | Charges YoY % | current vs prior-year growth % |
| 25 | Encounters Rolling 90 Days | `DATESINPERIOD` trailing 90-day count |
