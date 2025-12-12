# HMRC-Portfolio-Project

# 🏛️ HMRC Strategic Performance Monitor: Compliance & Operations

![Power BI](https://img.shields.io/badge/Power_BI-Desktop-yellow?style=for-the-badge&logo=power-bi)
![SQL](https://img.shields.io/badge/SQL-Data_Validation-blue?style=for-the-badge&logo=postgresql)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

## 📖 Client Background & Context

HMRC (Her Majesty's Revenue and Customs) is the UK government department responsible for the administration and collection of taxes, duties, and National Insurance. They play a critical role in funding public services and enforcing financial compliance for millions of individuals and businesses across the nation.

**The Scenario:**
HMRC is the UK’s tax, payments, and customs authority. Its primary purpose is to collect the money that pays for the UK’s public services and help families and individuals with targeted financial support. The organization faces a dual challenge: closing the "Tax Gap" (difference between tax due and collected) while modernizing customer service to reduce administrative costs.

**The Business Problem:**
HMRC leadership required a centralized BI solution to address three critical blockers:
1.  **Revenue Leakage:** While overall collection is high, specific sectors (Construction, Hospitality) show disproportionate signs of high-risk debt.
2.  **Operational Strain:** Call centers are overwhelmed with **24+ minute wait times**, primarily driven by simple, repetitive queries regarding Penalty Appeals.
3.  **Audit Efficiency:** The Internal Audit team lacked a data-driven method to prioritize which of the 2,000+ entities to investigate first.

---

## 📑 Table of Contents
1. [Executive Summary & Impact](#-executive-summary--quantified-impact)
2. [Key Business Questions Solved](#-key-business-questions-solved)
3. [Data Structure & Modelling](#-data-structure--modelling)
4. [Dashboard Deep Dive](#-dashboard-deep-dive)
5. [Strategic Recommendations](#-strategic-recommendations)
6. [Technical Implementation](#-technical-implementation--expertise)
7. [Data Dictionary](#-data-dictionary)
8. [Assumptions & Future Scope](#-assumptions--future-scope)

---

## 🏆 Executive Summary & Quantified Impact
This analysis integrated Revenue, Operations, and Risk data to provide a holistic performance view.

*   **Revenue Performance:** Achieved a **113.5% Collection Rate**, recovering £22bn against £19bn due. The surplus is driven by aggressive recovery of historical arrears in the <£50k income bands.
*   **Operational Bottleneck:** Identified a critical service failure with **Average Wait Times of ~24.6 minutes** and a CSAT score of **50%**.
*   **Risk Detection:** Flagged **2,000 High-Risk Taxpayers**, with the **Construction Sector** accounting for the largest share of high-risk debt.

---

## 🎯 Key Business Questions Solved
*   **Where is the revenue surplus coming from?**
    *   Analysis of Income Bands reveals that the **<30k** and **30k-50k** brackets have over-performed significantly in payments vs. due amounts.
*   **Why are customers frustrated?**
    *   **40%** of all calls are related to **"Penalty Appeals."** This volume is clogging the phone lines, driving wait times up to 24 minutes.
*   **Who should we audit next?**
    *   Constructed a "Hit List" of the Top 50 Taxpayers with high Audit Risk Scores (>90) and high outstanding Tax Gaps.

---

## 🗂 Data Structure & Modelling
Designed a **Star Schema** data model to enable cross-filtering between Operations, Revenue, and Filing data.

*   **`HMRC TAX_PAYER` (Dimension):** Core entity details including Sector, Region, Age Group, and the calculated Audit Risk Score.
*   **`HMRC FACT_FILING` (Fact):** Transactional data on tax filings, including Deadlines, Filing Methods (Digital/Paper), and Penalty Amounts.
*   **`HMRC FACT_OPERATION` (Fact):** Call center metrics including Wait Time, Duration, Topics, and CSAT scores.
*   **`HMRC TAXDUE/TAXPAID` (Fact):** Financial ledger tracking Amount Due vs Amount Paid.

---

## 🖼️ Dashboard Deep Dive

### 1. Executive Compliance Overview
*A high-level health check of the UK Tax System designed for the CFO.*
![Compliance Dashboard](Screenshot/1.Executive_Compliance_Overview.png)
*   **KPI Cards:** Immediate visibility on the £3bn Surplus Gap and 113.5% Collection Rate.
*   **Income Band Heatmap (Table):** Used data bars to visually highlight that the bulk of revenue flows from the lower-income bands (<£50k), whereas High Net Worth Individuals (100k+) have a lower collection volume.
*   **High Risk Debt by Sector (Bar Chart):** Clearly identifies **Construction** and **Hospitality** as the sectors with the highest exposure to high-risk debt, signaling where audit resources should be focused.

### 2. Operation & Customer Experience
*Diagnosing the root cause of the low 50% CSAT score.*
![Operations Dashboard](Screenshot/2.Operation_&_Customer_Experience.png)
*   **Call Volume Analysis (Donut Chart):** The most critical insight on the page. It reveals that **39.9%** of calls are for "Penalty Appeals." This is a process that could be automated.
*   **Wait Time Trends (Line Chart):** Shows cyclical spikes in wait times, correlating with filing deadlines (Jan/Feb). This helps Workforce Planning schedule staff more effectively.
*   **CSAT by Channel (Bar Chart):** Shows that "Phone" remains the dominant channel despite having lower satisfaction than digital channels.

### 3. Risk & Audit Intelligence
*An interactive "Workbench" for the Internal Audit team.*
![Risk Dashboard](Screenshot/3.Risk_&_Audit.png)
*   **Risk Matrix (Scatter Plot):** Plots `Audit Risk Score` (Y-Axis) vs `Tax Gap` (X-Axis). Using quadrant analysis, auditors can spot outliers (High Score + High Gap) immediately.
*   **Decomposition Tree:** Allows the user to drill down into the £1.3bn High Risk Debt by Region -> Sector -> Filing Method to find the root cause.
*   **Top 50 Target List (Table):** A generated "Hit List" of specific Taxpayer IDs that require immediate investigation, sorted by Risk Score.

---

## 💡 Strategic Recommendations

### 1. Operational: The "Digital Deflection" Strategy
*   **Finding:** 40% of calls are for Penalty Appeals, causing 24-minute wait times.
*   **Recommendation:** Launch a proactive SMS campaign 7 days before deadlines with a direct link to the "Digital Penalty Appeal" form.
*   **Impact:** Reduce call volume by an estimated 15%, improving CSAT and lowering wait times.

### 2. Audit: Sector-Specific Task Force
*   **Finding:** The Construction sector has the highest volume of High-Risk Debt.
*   **Recommendation:** Reallocate 20% of audit resources to specifically target Construction SMEs in the North West region.

### 3. CX: Push Web Chat Adoption
*   **Finding:** Phone is the highest volume channel despite Digital Adoption being only 50%.
*   **Recommendation:** Place the Web Chat button prominently on the "Penalty Appeal" landing page to deflect voice calls.

---

🧠 Assumptions & Future Scope
Assumptions:
Negative Tax Gap: The data shows a surplus (Negative Gap). It is assumed this includes the recovery of debts from previous financial years.
CSAT Scale: Assumed CSAT is an aggregate score out of 100 based on the raw data distribution.
Future Scope:
Sentiment Analysis: Integrate text analytics on "Call Topics" to understand specific "Form Confusion" pain points.
Predictive Auditing: Use Python/Machine Learning to predict which Taxpayers in the "Retail" sector are most likely to underpay next quarter based on filing history.


---

## 🛠 Technical Implementation & Expertise

### Data Cleaning (Power Query)
*   **Wait Time Correction:** Raw data contained negative timestamps due to system logging errors (e.g., `-145 mins`). Used Power Query `Table.TransformColumns` with `Number.Abs` to clean these into positive values.
*   **Risk Scoring:** Generated realistic Audit Risk Scores (1-100) using custom M-Code logic to replace placeholder sequential data.

---


📚 Data Dictionary
Table
Column
Description
HMRC TAX_PAYER
AuditRiskScore
Internal score (0-100) predicting likelihood of non-compliance.
HMRC TAX_PAYER
Sector
Industry classification (e.g., Construction, Retail).
HMRC FACT_FILING
PenaltyAmount
Financial penalty levied for late submissions.
HMRC FACT_OPERATION
Avg Wait Time (Corrected)
Time in minutes a customer waits in queue (Cleaned using ABS).
HMRC FACT_OPERATION
CSAT_Score
Customer Satisfaction Score (Normalized to 0-100%).
HMRC TAXDUE/TAXPAID
Tax Gap
Calculated as AmountDue - AmountPaid. Negative values indicate surplus collection.


---
