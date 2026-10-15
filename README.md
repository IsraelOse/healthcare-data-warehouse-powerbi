# Healthcare Data Warehouse & Power BI Dashboard

A dimensional (Kimball star-schema) data warehouse for hospital encounters with an interactive Power BI report: seven conformed dimensions around a 1,500-row `FactEncounter`, and **25 DAX measures** spanning every required function family.

## Data model
Star schema — see the full [data dictionary](docs/DATA_DICTIONARY.md).

```
                DimDate (admission + discharge roles)
                     |
 DimPatient --\      |      /-- DimProvider
 DimDiagnosis --\    |    /-- DimFacility
 DimProcedure ----  FactEncounter  ---- DimPayer
                 (1,500 encounters)
```

- **Fact:** FactEncounter (1,500 rows) — charges, cost, length of stay, readmission flag.
- **Dimensions:** Date (1,096), Patient (500), Provider (100), Facility (10), Diagnosis (20), Procedure (15), Payer (5).

## DAX measures
25 measures across five families (counting, math/statistical, logical, CALCULATE filter-context, time intelligence) — full catalogue with logic in [docs/MEASURES.md](docs/MEASURES.md).

## Report pages
1. **Model Validation** — schema and data-quality checks
2. **Executive Overview** — headline KPIs
3. **Clinical Overview** — readmission and procedure analysis
4. **Financial Overview** — charges, cost, margin

## Key findings (from the report)
- **Discharge dates were unreliable for 24.9%** of encounters (e.g. `20211040`, month 10 day 40); regenerated from AdmissionDate + LengthOfStay rather than dropped.
- **Imaging readmits at ~20.1%**, versus Surgery 14.1% and Lab 13.9%; Pediatrics (18.0%) and Cardiology (16.9%) sit above the 18% alert threshold.
- **Margin % is flat (~39.6–39.7%) across facility types**; clinics differ from hospitals by volume (787 vs 713 encounters), not efficiency.
- **Lab work is 44.9% of total billing** ($36.29M total) while being the lowest-readmission category.

## Contents
| Path | What it is |
|------|-----------|
| `Healthcare_DataWarehouse.pbix` | Power BI report (open in Power BI Desktop) |
| `Healthcare_DW_Report.pdf` | Written report |
| `data/` | Star-schema source tables (fact + 7 dimensions) |
| `docs/` | Data dictionary and DAX measure catalogue |

## Viewing
Open the `.pbix` in **Power BI Desktop** (free). A PDF export of the report is included for anyone without Power BI.

## Tech
Power BI · DAX · dimensional modelling (Kimball star schema)

*Individual assignment, CPSC-510 Data Warehousing & Visualization, Master of Data Analytics, University of Niagara Falls Canada.*
