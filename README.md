# Credit Card Fraud Analysis Dashboard

## Project Overview

This repository contains a Power BI dashboard for analyzing credit card fraud patterns based on transaction data. The dashboard visualizes key metrics such as transaction volumes, fraud rates, amounts by location, and breakdowns by transaction type (Purchase/Refund). It helps fraud analysts and risk managers identify anomalies, monitor trends over quarters, and make data-driven decisions to mitigate losses.

Built using Power BI with DAX formulas for KPIs and interactive visuals. The dashboard assumes a dataset table named `'Dataset'` with columns like `TransactionID`, `TransactionDate`, `Amount`, `MerchantID`, `TransactionType`, `Location`, and `IsFraud`. You can import a `.pbix` file (if provided) or recreate it using the DAX code below.

### Key Features
- **KPIs**: Fraud Rate, Average Fraud Amount, Total Transactions, Total Purchases/Refunds.
- **Charts**: Line charts for amounts by location, donut/pie for distributions, stacked bars for fraud by type, bar charts for counts by location.
- **Interactivity**: Slicers for TransactionType, Location, and Quarter (Q1-Q4).
- **Data Source**: CSV/Excel import (e.g., transaction logs with fraud flags).
- **Tools Used**: Power BI Desktop.

## Installation and Setup

1. Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free from Microsoft).
2. Import your dataset (e.g., `credit_card_fraud.csv`) via **Get Data > Text/CSV**.
3. In Power Query Editor, parse `TransactionDate` to Date format and create a Quarter column if needed (e.g., `= Date.QuarterOfYear([TransactionDate])`).
4. Add the DAX measures below under **Modeling > New Measure**.
5. Build visuals: Use the chart ideas from the screenshot (e.g., donut for amounts by location).
6. Add slicers: `TransactionType`, `Location`, and a custom Quarter slicer.
7. Publish to Power BI Service for sharing.

## Dashboard Screenshot

<img width="1185" height="700" alt="image" src="https://github.com/user-attachments/assets/d9a05a72-5045-4f3e-8c50-276ec4842de9" />

*(Upload the provided image as `dashboard-screenshot.png` in your repo. It shows the interactive dashboard with KPIs, charts, and slicers for locations like Chicago, Dallas, Houston, Los Angeles, New York, Philadelphia, Phoenix, and San Antonio.)*

## DAX Code

Copy-paste these measures directly into Power BI's "New Measure" dialog. They reference the `'Dataset'` table and use fields like `Amount`, `IsFraud`, `Location`, `TransactionType`, and `TransactionDate`.

### Count of TransactionID (Total Transactions)
```dax
Count of TransactionID = COUNTROWS('Dataset')Average Fraud Amount
daxAvg Fraud Amount = CALCULATE(AVERAGE('Dataset'[Amount]), 'Dataset'[IsFraud] = 1)
Fraud Rate
daxFraud Rate = 
DIVIDE(
    SUM('Dataset'[IsFraud]),
    COUNTROWS('Dataset')
) * 100
Total Purchases
daxTotal Purchases = COUNTROWS(FILTER('Dataset', 'Dataset'[TransactionType] = "Purchase"))
Total Refunds
daxTotal Refunds = COUNTROWS(FILTER('Dataset', 'Dataset'[TransactionType] = "Refund"))
Sum of Transaction Amount by Location
daxSum of Transaction Amount by Location = SUM('Dataset'[Amount])
Count of TransactionID by Location
daxCount of TransactionID by Location = COUNTROWS('Dataset')
Avg Fraud Amount and Count of TransactionID by TransactionType
daxAvg Fraud Amount by Type = CALCULATE(AVERAGE('Dataset'[Amount]), 'Dataset'[IsFraud] = 1)
