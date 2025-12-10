-- 1. REVENUE COLLECTION CHECK  
-- Verifying the 113.5% Collection Rate  
SELECT   
    SUM(AmountDue) AS Total_Due,  
    SUM(AmountPaid) AS Total_Paid,  
    (SUM(AmountPaid) * 1.0 / NULLIF(SUM(AmountDue),0)) * 100 AS Collection_Rate  
FROM [HMRC TAXDUE/TAXPAID];  
  
  
  
-- 2. OPERATIONAL BOTTLENECKS  
-- Identifying the top reasons for calls to the contact center  
SELECT   
    Topic AS Call_Reason,  
    COUNT(CallID) AS Total_Calls,  
    AVG(ABS(WaitTime_Min)) AS Avg_Wait_Time -- Using ABS to handle data anomalies  
FROM [HMRC FACT_OPERATION]  
GROUP BY Topic  
ORDER BY Total_Calls DESC;  
  
  
  
-- 3. RISK PROFILING (AUDIT TARGETS)  
-- Identifying sectors with the highest High Risk Debt  
SELECT   
    tp.Sector,  
    AVG(tp.AuditRiskScore) AS Avg_Risk_Score,  
    SUM(td.AmountDue) AS Total_Debt_Exposure  
FROM [HMRC TAX_PAYER] tp  
JOIN [HMRC TAXDUE/TAXPAID] td ON tp.TaxpayerID = td.TaxpayerID  
WHERE tp.AuditRiskScore > 70  
GROUP BY tp.Sector  
ORDER BY Total_Debt_Exposure DESC;  
  
  
  
-- 4. DIGITAL ADOPTION  
-- Calculating the ratio of Digital vs Paper filings  
SELECT   
    FilingMethod,  
    COUNT(FilingID) AS Count,  
    (COUNT(FilingID) * 100.0 / (SELECT COUNT(*) FROM [HMRC FACT_FILING])) AS Pct_Share  
FROM [HMRC FACT_FILING]  
GROUP BY FilingMethod;  
