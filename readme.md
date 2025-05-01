Info Tech Projects Spring 25

Company: Daisy Chain Energy

Members: 
Flynn Wei, 
Harsh Pooniwala, 
Tianle Yang, 
Xiyuan Jiang


This repository contains a set of Google Colab notebooks designed to analyze electricity usage, simulate solar PV output, estimate billing under ConEd’s SC9.1 tariff, and present results through an interactive dashboard.

All required files and outputs for running the dashboard are located in the `FINAL` folder.

---

## 📋 Workflow Overview

Run the notebooks **in the following order**, using Google Colab:

---

### 1. `raw_meter_data_ex.ipynb`

**Purpose**  
- Processes raw 15-minute electricity data (2021–2024)
- Detects zero-value gaps
- Aggregates into a clean hourly format (for 2023–2024)

**Required Input**  
- `rawMeterData-123W93Street.xls` (Excel with sheets: `2021`, `2022`, `2023`, `2024`)

**Outputs Generated**  
- `combined_meter_data.csv`  
- `zero_gap_report.csv`  
- `nonzero_subset_2023_2024.csv`  
- `hourly_consumption_backfilled_2023_2024.csv`

---

### 2. `weather_analysis.ipynb`

**Purpose**  
- Cleans and reformats hourly NSRDB weather and irradiance data for NYC

**Required Input**  
- `weather_csv.csv`  
  *(Expected columns: Year, Month, Day, Hour, Minute, GHI, DNI, DHI, Temperature, Wind Speed)*

**Output Generated**  
- `nsrdb_weather_nyc_2023_hourly.csv`

---

### 3. `PVmodel_merge.ipynb`

**Purpose**  
- Simulates hourly PV generation using `pvlib`  
- Merges building load with weather and PV data

**Required Inputs**  
- `hourly_consumption_backfilled_2023_2024.csv`  
- `nsrdb_weather_nyc_2023_hourly.csv`

**Output Generated**  
- `merged_hourly_with_pv.csv`

---

### 4. `Billing_Estimation.ipynb`

**Purpose**  
- Calculates monthly bills with and without PV using SC9.1 tariff  
- Estimates energy and cost savings

**Required Input**  
- `merged_hourly_with_pv.csv`

**Output Generated**  
- `monthly_bills.csv`

---

### 5. `dashboard.ipynb`

**Purpose**  
- Launches an interactive Streamlit dashboard to explore financial models, billing insights, PV generation, and weather-load trends

**Required Inputs**  
- `merged_hourly_with_pv.csv`  
- `monthly_bills.csv`  
- `nsrdb_weather_nyc_2023_hourly.csv`

**Output**  
- None (dashboard runs in-browser)

---

## 🌐 Hosting the Dashboard

The final cell in `dashboard.ipynb` uses **ngrok** to expose the dashboard via a public URL.

> ⚠️ If the default ngrok token is invalid or rate-limited:
> - [Create an ngrok account](https://dashboard.ngrok.com/signup)
> - Generate your personal auth token
> - Replace the command in the notebook:
>
> ```bash
> !ngrok config add-authtoken <your_token_here>
> ```

You can also replace the last cell with any other hosting method, such as:
- Running `streamlit run app.py` locally
- Hosting on a VM or cloud platform (e.g., Heroku)

---

## 📁 Summary of Input/Output Files

| Notebook               | Input(s)                                           | Output(s)                                                                 |
|------------------------|----------------------------------------------------|---------------------------------------------------------------------------|
| raw_meter_data_ex      | `rawMeterData-123W93Street.xls`                   | `combined_meter_data.csv`, `zero_gap_report.csv`, `nonzero_subset_2023_2024.csv`, `hourly_consumption_backfilled_2023_2024.csv` |
| weather_analysis        | `weather_csv.csv`                                 | `nsrdb_weather_nyc_2023_hourly.csv`                                       |
| PVmodel_merge           | `hourly_consumption_backfilled_2023_2024.csv`, `nsrdb_weather_nyc_2023_hourly.csv` | `merged_hourly_with_pv.csv`                           |
| Billing_Estimation      | `merged_hourly_with_pv.csv`                      | `monthly_bills.csv`                                                       |
| dashboard               | `merged_hourly_with_pv.csv`, `monthly_bills.csv`, `nsrdb_weather_nyc_2023_hourly.csv` | (visual interface only)                            |

---

## ✅ Final Notes

- All processing and visualization is designed for Colab.
- Ensure that inputs are uploaded to the Colab environment as needed.
- Intermediate CSV outputs should be downloaded after each notebook, then uploaded into the next step.

---
