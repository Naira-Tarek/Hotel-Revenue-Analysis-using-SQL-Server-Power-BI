# 📊 Hotel Revenue Analysis using SQL Server & Power BI

This project showcases an end-to-end analysis pipeline for hotel bookings from 2018 to 2020. The goal was to calculate hotel revenue, analyze customer behavior, and present insights using SQL and Power BI.

## 🗂️ Dataset
- Excel file containing 3 sheets: `2018`, `2019`, and `2020`.
- Each row represents a hotel booking with details like:
  - Hotel type, arrival date, nights stayed, price per night (ADR), cancellation, customer type, etc.

## 🛠 Tools Used
- Microsoft SQL Server 2019
- Power BI
- Excel

## ⚙️ Process
1. **Imported and combined data from Excel sheets using SQL**
2. **Created revenue calculations:**
```sql
SELECT * FROM dbo.['2018$']
   
SELECT * FROM dbo.['2019$']
    
SELECT * FROM dbo.['2020$']

WITH hotels AS (
    SELECT * FROM dbo.['2018$']
    UNION
    SELECT * FROM dbo.['2019$']
    UNION
    SELECT * FROM dbo.['2020$']
)


SELECT 
arrival_date_year,hotel,
round(sum((stays_in_week_nights + stays_in_weekend_nights) * adr),2) AS revenue
FROM hotels
group by arrival_date_year,hotel



select * from hotels
left join dbo.market_segment$
on hotels.market_segment=market_segment$.market_segment
left join 
dbo.meal_cost$
on meal_cost$.meal=hotels.meal
