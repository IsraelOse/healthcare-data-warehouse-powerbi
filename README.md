# Healthcare Data Warehouse & Power BI Dashboard

A dimensional (star-schema) data warehouse for healthcare encounters, with an interactive Power BI report on top.

## Design
- **Star schema:** a central `FactEncounter` table (~1,500 encounters) surrounded by dimensions — Patient, Provider, Facility, Payer, Diagnosis, Procedure, Date
- **38 DAX measures** for KPIs across cost, volume, and outcomes
- Multiple report pages for different analytical views

## Repo layout
| Path | What it is |
|------|-----------|
| `Healthcare_DataWarehouse.pbix` | Power BI report (open in Power BI Desktop) |
| `Dim*.csv`, `FactEncounter.csv` | Star-schema source tables |
| `Healthcare_DW_Report.pdf` / `.docx` | Written report |
| `Assignment_Brief.pdf` | Original assignment specification |

## View it
Open the `.pbix` in **Power BI Desktop** (free). A PDF export of the report is included for anyone without Power BI.

## Tech
Power BI · DAX · dimensional modelling (Kimball-style star schema)

*Individual assignment, CPSC-510 Data Warehousing & Visualization, Master of Data Analytics.*
