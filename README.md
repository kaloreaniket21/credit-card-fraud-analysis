# 🚨 Credit Card Fraud Detection & Risk Analytics Dashboard

[![Power BI](https://img.shields.io/badge/Data_Viz-Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Excel](https://img.shields.io/badge/Data_Processing-MS%20Excel-217346?style=flat&logo=microsoftexcel&logoColor=white)](https://www.microsoft.com/excel)
[![Domain](https://img.shields.io/badge/Domain-Financial_Risk-red?style=flat)](#)

A diagnostic analytics project built to monitor, detect, and analyze fraudulent credit card transactions. This Power BI dashboard helps risk management teams rapidly identify compromised merchants, geographic fraud hotspots, and anomalous transaction behaviors.

## 🌟 Project Overview
Credit card fraud exposes financial institutions to direct revenue loss and damages customer trust. While automated algorithms block transactions in real-time, risk analysts require post-incident visibility to understand *how* algorithms are failing or to investigate suspicious batches of data. 

This project transforms raw transactional logs into an interactive visual risk-monitoring tool, allowing analysts to quickly filter out legitimate transactions and focus entirely on anomalous patterns.

### Key Business Questions Answered:
* What is the total financial exposure (dollar amount) lost to fraudulent transactions?
* Which specific merchants (`MerchantID`) are experiencing the highest volume of compromised transactions?
* Are bad actors exploiting standard "Purchases" or manipulating the "Refund" system?
* Are there specific geographic regions (`Location`) showing disproportionate fraud rates?

---

## 🛠 Tech Stack & Workflow
* **Data Processing & ETL:** **Microsoft Excel / Power Query** used to parse complex `TransactionDate` time-stamps, handle missing values, and verify the binary `IsFraud` flag.
* **Data Modeling:** **Power BI Desktop** used to structure the fact table and establish reporting hierarchies.
* **Calculations:** **DAX (Data Analysis Expressions)** utilized to engineer dynamic risk KPIs.
* **Visualization:** **Power BI** interactive dashboard featuring geographic mapping and cross-filtering.

---

## 📊 Dashboard Features
The dashboard interface is designed specifically for risk analysts, utilizing a high-contrast color palette (Red for fraud, standard colors for baseline data) for rapid cognitive processing.

<img width="1269" height="702" alt="Screenshot 2026-03-06 114705" src="https://github.com/user-attachments/assets/a5caf9c6-ab52-4192-9658-e19eacce2f1b" />
<img width="1262" height="701" alt="Screenshot 2026-03-06 114716" src="https://github.com/user-attachments/assets/873431b1-69c7-4ac7-8784-83966cf1fd77" />


1. **Executive Risk KPIs:**
   * Total Transaction Volume
   * Fraudulent Transaction Count
   * Overall Fraud Rate (%)
   * Total Financial Exposure ($)

2. **Geospatial & Vendor Analysis:**
   * **Map Visual:** Maps total fraud amounts across different `Location`s (e.g., New York, Dallas).
   * **Merchant Vulnerability Chart:** Ranks the Top 10 `MerchantID`s by fraud volume to flag compromised payment gateways.

3. **Behavioral Breakdown:**
   * **Donut Charts:** Segments fraud by `TransactionType` (Purchase vs. Refund).
   * **Scatter Plot / Distribution:** Analyzes transaction `Amount` to differentiate between automated "micro-transaction" card testing and high-value theft.

---

## 🚀 How to Run This Project
1. **Download the Repository:** Clone this repo or download the `.pbix` file.
2. **Prerequisites:** Ensure you have the latest version of [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/) installed.
3. **Interact:** Open the `.pbix` file. Use the `IsFraud` slicer to toggle between viewing legitimate baseline data and isolated fraudulent records.

---

## ⚙️ DAX (Data Analysis Expressions) Implementation
To enable dynamic filtering and accurate financial tracking, several custom DAX measures were engineered for the KPI scorecards. Here are the core formulas used in this project:

```dax
-- 1. Total Baseline Transactions
Total Transactions = COUNTROWS('FraudData')

-- 2. Total Fraudulent Transactions
Fraud Count = CALCULATE(
    COUNTROWS('FraudData'), 
    'FraudData'[IsFraud] = 1
)

-- 3. Overall Fraud Rate Percentage
Fraud Rate % = DIVIDE(
    [Fraud Count], 
    [Total Transactions], 
    0
)

-- 4. Total Financial Exposure (Sum of Fraudulent Amounts)
Total Fraud Amount = CALCULATE(
    SUM('FraudData'[Amount]), 
    'FraudData'[IsFraud] = 1
)

-- 5. Average Fraud Ticket Size
Avg Fraud Amount = CALCULATE(
    AVERAGE('FraudData'[Amount]), 
    'FraudData'[IsFraud] = 1
)
