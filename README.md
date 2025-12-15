<div align="center">

# 🏛️ HMRC Strategic Performance Monitor
### Compliance, Audit & Operations Intelligence


| **Tech Stack** | **Methodology** | **Project Status** |
|:---:|:---:|:---:|
| <img src="https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" /> | <img src="https://img.shields.io/badge/Star_Schema-blue?style=for-the-badge" /> | <img src="https://img.shields.io/badge/Complete-success?style=for-the-badge" /> |
| <img src="https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white" /> | <img src="https://img.shields.io/badge/DAX-green?style=for-the-badge" /> | **2023 - 2024** |

</div>

> **Disclaimer:** This is a personal portfolio project using a synthetic dataset. It is a simulation of real-world public sector challenges and is not affiliated with His Majesty's Revenue and Customs.
---

## 📋 Mission Directive: Closing the Tax Gap

**Department:** Operational Excellence & Revenue Protection  
**Focus:** Risk Identification, Debt Recovery & Service Optimization

> *"To collect the money that pays for the UK’s public services and help families and individuals with targeted financial support."*

### 🔻 The Challenge
HMRC faces a dual-pressure environment: maximizing revenue collection while minimizing administrative friction. Leadership identified that the **"Tax Gap"** (the difference between tax owed and tax collected) was widening in specific sectors, while customer service channels were buckling under repetitive inquiries.

### ⚠️ Critical Blockers Identified
1.  **Fiscal Risk:** While overall collection is high, specific sectors (Construction, Hospitality) show disproportionate signs of high-risk debt ("The Ghost Economy").
2.  **Citizen Friction:** Call centers are overwhelmed with **24+ minute wait times**, primarily driven by simple, repetitive queries regarding Penalty Appeals.
3.  **Audit Allocation:** The Internal Audit team lacked a data-driven method to prioritize which of the 2,000+ entities to investigate first.

---

## 📑 Table of Contents
1. [Executive Summary & Impact](#-executive-summary--quantified-impact)
2. [Key Business Questions Solved](#-key-business-questions-solved)
3. [Data Structure & Modelling](#-data-structure--modelling)
4. [Dashboard Deep Dive](#-dashboard-deep-dive)
5. [Strategic Recommendations](#-strategic-recommendations)
6. [Technical Implementation](#-technical-implementation--expertise)

---

## 🏆 Executive Summary & Quantified Impact

This analysis integrated Revenue, Operations, and Risk data to provide a holistic performance view for the Permanent Secretary and CFO.

| Metric | Result | Impact |
| :--- | :--- | :--- |
| **Revenue Collection** | **113.5%** | Recovered **£22bn** against £19bn due, driven by aggressive arrears recovery in <£50k bands. |
| **Service Level** | **24.6 mins** | Identified critical failure in average wait times, correlating to a low **50% CSAT** score. |
| **Risk Detection** | **2,000** | Flagged 2,000 high-risk taxpayers, with **Construction** accounting for the largest share of exposure. |

---

## 🎯 Key Business Questions Solved

**1. Where is the revenue surplus coming from?**
> Analysis of Income Bands reveals that the **<£30k** and **£30k-£50k** brackets have over-performed significantly in payments vs. due amounts. This suggests successful recovery of historical debt in the lower income brackets.

**2. Why are citizens frustrated (Low CSAT)?**
> **39.9%** of all calls are related to **"Penalty Appeals."** This specific query volume is clogging phone lines, driving wait times up to 24 minutes and blocking urgent complex queries.

**3. Who should the Audit Team target next?**
> Constructed a **"Hit List"** of the Top 50 Taxpayers with Audit Risk Scores >90 and high outstanding Tax Gaps.

---

## 🗂 Data Structure & Modelling

Designed a **Star Schema** architecture to enable cross-filtering between Operations, Revenue, and Filing data.

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
*   **Income Band Heatmap:** Visually highlights that the bulk of revenue flows from the lower-income bands (<£50k), whereas High Net Worth Individuals (100k+) have a lower collection volume.
*   **Sector Risk:** Clearly identifies **Construction** and **Hospitality** as the sectors with the highest exposure to high-risk debt.

### 2. Operation & Citizen Experience
*Diagnosing the root cause of the low 50% CSAT score.*
![Operations Dashboard](Screenshot/2.Operation_&_Customer_Experience.png)
*   **Call Volume Analysis:** The most critical insight. **39.9%** of calls are for "Penalty Appeals." This is a process that could be automated.
*   **Wait Time Trends:** Shows cyclical spikes in wait times, correlating with filing deadlines (Jan/Feb).
*   **CSAT by Channel:** Shows that "Phone" remains the dominant channel despite having lower satisfaction than digital channels.

### 3. Risk & Audit Intelligence
*An interactive "Workbench" for the Internal Audit team.*
![Risk Dashboard](Screenshot/3.Risk_&_Audit.png)
*   **Risk Matrix (Scatter Plot):** Plots `Audit Risk Score` (Y-Axis) vs `Tax Gap` (X-Axis). Auditors can spot outliers (High Score + High Gap) immediately.
*   **Decomposition Tree:** Drills down into the £1.3bn High Risk Debt by Region -> Sector -> Filing Method to find the root cause.
*   **Target List:** A generated "Hit List" of specific Taxpayer IDs that require immediate investigation.

---

## 💡 Strategic Recommendations

### 1. Operational: The "Digital Deflection" Strategy
*   **Finding:** 40% of calls are for Penalty Appeals, causing 24-minute wait times.
*   **Recommendation:** Launch a proactive SMS campaign 7 days before deadlines with a direct link to the "Digital Penalty Appeal" form.
*   **Impact:** Reduce call volume by an estimated **15%**, improving CSAT and lowering wait times.

### 2. Audit: Sector-Specific Task Force
*   **Finding:** The Construction sector has the highest volume of High-Risk Debt.
*   **Recommendation:** Reallocate **20%** of audit resources to specifically target Construction SMEs in the North West region.

---

## 🛠 Technical Implementation & Expertise

### Data Cleaning (Power Query / M)
*   **Wait Time Correction:** Raw data contained negative timestamps due to legacy system logging errors (e.g., `-145 mins`).
    *   *Solution:* Used `Table.TransformColumns` with `Number.Abs` to clean these into positive values for accurate averaging.
*   **Risk Scoring:** Generated realistic Audit Risk Scores (1-100) using custom conditional logic to categorize entities based on payment history and sector risk.

### Data Dictionary
| Table | Column | Description |
| :--- | :--- | :--- |
| **HMRC_TAX_PAYER** | `AuditRiskScore` | Internal score (0-100) predicting likelihood of non-compliance. |
| **HMRC_TAX_PAYER** | `Sector` | Industry classification (e.g., Construction, Retail). |
| **HMRC_FACT_FILING** | `PenaltyAmount` | Financial penalty levied for late submissions. |
| **HMRC_FACT_OPERATION** | `Avg_Wait_Time` | Time in minutes a customer waits in queue (Cleaned using ABS function). |
| **HMRC_TAXDUE** | `Tax_Gap` | Calculated as `AmountDue - AmountPaid`. Negative values indicate surplus collection. |

---
### 🧠 Assumptions & Future Scope
*   **Negative Tax Gap:** The data shows a surplus. It is assumed this includes the recovery of debts from previous financial years.
*   **Future Scope:** Integrate Sentiment Analysis on "Call Topics" to understand specific "Form Confusion" pain points using Python text analytics.




---
