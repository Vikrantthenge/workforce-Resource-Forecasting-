# Workforce & Resource Forecasting Tool  
### Excel • Python • Power BI

A complete workforce planning and forecasting system built using a synthetic but highly realistic operational dataset covering:  
- Hourly workload (180 days)  
- Forecasted demand (next 30 days)  
- Staffing requirements  
- Shift capacity  
- SLA risk  
- Backlog tracking  

This project demonstrates end-to-end capability in **capacity planning**, **forecasting**, **SLA modeling**, and **operational analytics**.

---

## 📌 Project Overview

This Workforce & Resource Forecasting Tool helps answer critical operational questions:

- How much workload should we expect tomorrow or next month?  
- How many agents do we need to meet service levels?  
- Will staffing gaps lead to SLA failures?  
- What hours and days experience the highest load?  
- How do shrinkage, attendance, and occupancy affect operations?  

The project uses **Excel**, **Python**, and **Power BI**, making it suitable for Business Analyst, Ops Analyst, and Data Analyst roles.

---

# 🧩 Dataset Details

Two datasets were used:

### **1. HourlyData (workforce_forecast_dataset.csv)**  
- 180 days of hourly call volumes  
- Expected & actual workload  
- Required agents  
- Scheduled staff  
- Attendance rate  
- Available staff  
- Handled calls  
- Backlog  
- SLA met (1/0)

### **2. ForecastData (Workforce_Forecast_Final.csv)**  
- 30-day daily forecast using Prophet  
- ForecastVolume  
- RequiredAgents  
- ScheduledStaff (placeholder)  
- StaffingGap  
- SLA Risk (High / Low)

---

# 🔧 Tools Used

| Tool | Purpose |
|------|---------|
| **Excel** | Data review, pivoting, staffing formulas |
| **Python (Prophet)** | Forecasting next 30 days |
| **Power BI** | Dashboard & scenario simulation |
| **DAX** | Measures for KPIs & SLA modeling |

---

# 🧮 Python Forecasting (Prophet)

```python
from prophet import Prophet
import pandas as pd

df = pd.read_csv("workforce_forecast_dataset.csv", parse_dates=['Timestamp'])

daily = df.groupby(df['Timestamp'].dt.date)['ActualVolume'].sum().reset_index()
daily.columns = ['ds', 'y']

model = Prophet(daily_seasonality=True, weekly_seasonality=True)
model.fit(daily)

future = model.make_future_dataframe(periods=30)
forecast = model.predict(future)
forecast.to_csv("forecast_output_30days.csv", index=False)
