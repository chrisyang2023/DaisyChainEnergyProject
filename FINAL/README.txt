============================================================
Solar Energy Savings Analysis Dashboard - DAISYCHAIN
============================================================

This project includes a series of Google Colab notebooks for analyzing electricity usage, modeling solar PV output, estimating billing under ConEd’s SC9.1 tariff, and visualizing results via an interactive Streamlit dashboard.

The entire workflow is designed to be run on Colab. Each notebook reads input CSV files and generates new outputs required for the next step.

------------------------------------------------------------
NOTEBOOK EXECUTION FLOW (Run in this order)
------------------------------------------------------------

1. raw_meter_data_ex.ipynb
------------------------------------------------------------
Purpose:
- Processes 15-minute interval electricity data from 2021–2024.
- Detects gaps (zero-value readings).
- Aggregates into a clean hourly profile (only for 2023–2024).

Required Input:
- rawMeterData-123W93Street.xls
  (Excel file with sheets named: 2021, 2022, 2023, 2024)

Generated Outputs:
- combined_meter_data.csv
- zero_gap_report.csv
- nonzero_subset_2023_2024.csv
- hourly_consumption_backfilled_2023_2024.csv

------------------------------------------------------------

2. weather_analysis.ipynb
------------------------------------------------------------
Purpose:
- Cleans and reformats hourly weather and irradiance data.

Required Input:
- weather_csv.csv
  (Columns must include: Year, Month, Day, Hour, Minute, GHI, DNI, DHI, Temperature, Wind Speed)

Generated Output:
- nsrdb_weather_nyc_2023_hourly.csv

------------------------------------------------------------

3. PVmodel_merge.ipynb
------------------------------------------------------------
Purpose:
- Simulates hourly PV output using pvlib.
- Merges weather and building load into one dataset.

Required Inputs:
- hourly_consumption_backfilled_2023_2024.csv
- nsrdb_weather_nyc_2023_hourly.csv

Generated Output:
- merged_hourly_with_pv.csv

------------------------------------------------------------

4. Billing_Estimation.ipynb
------------------------------------------------------------
Purpose:
- Calculates monthly bills under SC9.1 tariff.
- Compares baseline vs. post-PV cost and savings.

Required Input:
- merged_hourly_with_pv.csv

Generated Output:
- monthly_bills.csv

------------------------------------------------------------

5. dashboard.ipynb
------------------------------------------------------------
Purpose:
- Launches an interactive Streamlit dashboard.
- Allows financial modeling, billing insights, PV output analysis, and weather/load exploration.

Required Inputs:
- merged_hourly_with_pv.csv
- monthly_bills.csv
- nsrdb_weather_nyc_2023_hourly.csv

Generated Output:
- None (dashboard runs in browser)

------------------------------------------------------------
DASHBOARD HOSTING INSTRUCTIONS
------------------------------------------------------------

The final cell in dashboard.ipynb launches the Streamlit dashboard using ngrok, which provides a temporary public URL.

IMPORTANT:
- The current notebook uses a preset ngrok auth token.
- If the token fails or expires, please:
  (1) Visit https://dashboard.ngrok.com/signup
  (2) Create a free account and obtain your auth token.
  (3) Replace the line in the notebook:
      !ngrok config add-authtoken <your_token_here>

Alternative:
- You may use any other hosting method.
- Simply replace the final cell with the host of your choice (e.g., local streamlit run app.py, Heroku, etc.).

------------------------------------------------------------
INPUT AND OUTPUT SUMMARY
------------------------------------------------------------

Notebook: raw_meter_data_ex.ipynb
Input: rawMeterData-123W93Street.xls
Outputs:
- combined_meter_data.csv
- zero_gap_report.csv
- nonzero_subset_2023_2024.csv
- hourly_consumption_backfilled_2023_2024.csv

Notebook: weather_analysis.ipynb
Input: weather_csv.csv
Output:
- nsrdb_weather_nyc_2023_hourly.csv

Notebook: PVmodel_merge.ipynb
Inputs:
- hourly_consumption_backfilled_2023_2024.csv
- nsrdb_weather_nyc_2023_hourly.csv
Output:
- merged_hourly_with_pv.csv

Notebook: Billing_Estimation.ipynb
Input: merged_hourly_with_pv.csv
Output: monthly_bills.csv

Notebook: dashboard.ipynb
Inputs:
- merged_hourly_with_pv.csv
- monthly_bills.csv
- nsrdb_weather_nyc_2023_hourly.csv
Output: None

============================================================
End of Instructions
============================================================
