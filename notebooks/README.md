# Data

This project uses publicly available data from the Australian Energy Market Operator (AEMO).

## Analysis Period

1 August 2025 to 31 July 2026

## Data Sources

### Aggregated Price and Demand

AEMO Aggregated Price and Demand data for the Victorian NEM region (`VIC1`).

Fields used include:

- `SETTLEMENTDATE`
- `TOTALDEMAND`
- `RRP`
- `REGION`
- `PERIODTYPE`

Source:
https://www.aemo.com.au/

### DISPATCHSCADA

AEMO DISPATCHSCADA data was used to obtain five-minute unit-level generation values.

Daily archives were accessed from AEMO NEMWeb:

https://www.nemweb.com.au/REPORTS/ARCHIVE/Dispatch_SCADA/

The raw daily files contain nested five-minute ZIP/CSV files and were processed using Python.

### Generator Metadata

AEMO Generation Information data was used to map Dispatchable Unit Identifiers (DUIDs) to:

- Region
- Technology Type
- Site
- Dispatch Type
- Nameplate Capacity

Source:
https://www.aemo.com.au/energy-systems/electricity/national-electricity-market-nem/nem-forecasting-and-planning/forecasting-and-planning-data/generation-information

## Processed Dataset

`final_market_dataset.csv` contains the final five-minute analytical dataset used by the Power BI report and analysis notebook.

The dataset contains:

- 105,120 five-minute intervals
- Victorian wholesale RRP
- Total demand
- Coal generation
- Gas turbine generation
- Hydro generation
- Solar PV generation
- Wind generation
- Battery storage SCADA values
- Derived renewable and thermal generation fields
- Analytical demand and renewable-output groups

## Data Quality

Twenty DISPATCHSCADA generation intervals on 10 March 2026 were missing from the source data.

These timestamps were retained using the complete Price and Demand series as the master time index. Generation fields for those intervals were left missing rather than imputed.

## Raw Data

The complete collection of raw AEMO daily ZIP archives is not stored in this repository because it is large and can be obtained from AEMO/NEMWeb.

The Python processing notebook documents the extraction and transformation workflow.
