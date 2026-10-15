# Data Dictionary — Healthcare Data Warehouse

A Kimball-style **star schema**: one central fact table surrounded by seven conformed dimensions, joined on surrogate keys. Source tables are in [`../data/`](../data).

## Fact table

### FactEncounter — 1,500 rows
One row per patient encounter.

| Column | Type | Notes |
|--------|------|-------|
| EncounterID | key | Grain: one row per encounter |
| PatientID | FK → DimPatient | |
| ProviderID | FK → DimProvider | |
| FacilityID | FK → DimFacility | |
| DiagnosisID | FK → DimDiagnosis | |
| ProcedureID | FK → DimProcedure | |
| PayerID | FK → DimPayer | |
| AdmissionDateID | FK → DimDate | |
| DischargeDateID | FK → DimDate | 373 rows (24.9%) had invalid dates; regenerated from Admission + LengthOfStay |
| LengthOfStay | measure | Days |
| TotalCharges | measure | Gross amount billed (CAD/USD) |
| TotalCost | measure | Cost to deliver |
| ReadmissionFlag | flag | 1 = readmitted, 0 = not |

## Dimension tables

| Table | Rows | Columns |
|-------|-----:|---------|
| DimDate | 1,096 | DateID, FullDate, Year, Month, Quarter |
| DimPatient | 500 | PatientID, Gender, AgeGroup, State |
| DimProvider | 100 | ProviderID, Specialty, ProviderType |
| DimFacility | 10 | FacilityID, FacilityType, State, BedCount |
| DimDiagnosis | 20 | DiagnosisID, DiagnosisCategory |
| DimProcedure | 15 | ProcedureID, ProcedureCategory |
| DimPayer | 5 | PayerID, PayerType |

All dimensions relate one-to-many to FactEncounter on their surrogate ID; DimDate connects twice (admission and discharge roles).
