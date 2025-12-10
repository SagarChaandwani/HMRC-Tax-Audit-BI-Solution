# DAX Measures Documentation  
  
Below are the key DAX formulas used in the HMRC Performance Model.  
  
## 1. Revenue Metrics  
**Tax Gap (Surplus/Deficit)**  
```dax  
Tax Gap = SUM('HMRC TAXDUE/TAXPAID'[AmountDue]) - SUM('HMRC TAXDUE/TAXPAID'[AmountPaid])  
**Collection Rate %**  
****codeDax****  
Collection Rate = DIVIDE(SUM('HMRC TAXDUE/TAXPAID'[AmountPaid]), SUM('HMRC TAXDUE/TAXPAID'[AmountDue]), 0)  
  
  
  
  
**2. Operational Metrics**  
****CSAT %  ******Converts raw score to a percentage format.**  
****codeDax****  
CSAT % = [Avg CSAT Score] / 100  
**Avg Wait Time (Minutes)**  
****codeDax****  
Avg Wait Time = AVERAGE('HMRC FACT_OPERATION'[WaitTime_Min])  
  
  
  
**3. Risk Intelligence**  
****High Risk Debt ******Calculates outstanding debt only for taxpayers with a Risk Score > 70.**  
****codeDax****  
High Risk Debt =   
CALCULATE(  
    [Tax Gap],   
    FILTER('HMRC TAX_PAYER', 'HMRC TAX_PAYER'[AuditRiskScore] >= 70)  
)  
  
  
**4.Digital Adoption %**  
****codeDax****  
Digital Adoption % =   
VAR DigitalFilings = CALCULATE(COUNT('HMRC FACT_FILING'[FilingID]), 'HMRC FACT_FILING'[FilingMethod] = "Digital")  
VAR TotalFilings = COUNT('HMRC FACT_FILING'[FilingID])  
RETURN DIVIDE(DigitalFilings, TotalFilings, 0)  
