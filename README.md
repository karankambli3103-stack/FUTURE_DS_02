# 📊 Telco Customer Churn Analysis Dashboard (Power BI)

An executive-level Power BI dashboard built to analyze customer attrition, identify high-risk subscriber segments, and evaluate the revenue impact of churn across 28,142 customers.

![Telco Churn Dashboard](images/dashboard_preview.png)

---

## 🎯 Executive Summary & Key Metrics

* **Total Customer Base:** 28,142 subscribers (20,759 retained | 7,383 churned)
* **Overall Churn Rate:** **26.23%** (Benchmark baseline)
* **Contract Risk Concentration:** **88.7%** of all churned subscribers were on **Month-to-Month** contracts.
* **Pricing Gap:** Churned customers paid an average of **$73.97/mo** compared to **$61.29/mo** for retained customers (a ~$12.68 churn premium).
* **Early-Tenure Vulnerability:** First 6 months carry the steepest risk, exhibiting a **52.76% churn rate**.

---

## 🔍 Core Business Insights

1. **The Month-to-Month Contract Trap:**
   * Month-to-month contracts account for **6,551 out of 7,383** churned users. Annual and two-year commitments drop churn share to 8.7% and 2.5% respectively.
2. **First-Year Onboarding Gap:**
   * Churn rate drops rapidly with customer tenure:
     * **0–6 Months:** 52.76% (Critical risk zone)
     * **6–12 Months:** 35.61%
     * **12+ Months:** 16.82% (Well below the 26.24% baseline)
3. **Value vs. Cost Disconnect:**
   * Higher average monthly bills among churned users indicate churn is often driven by perceived cost-to-value friction rather than inactive or low-spend accounts.
4. **Value-Added Service Retention:**
   * Accounts without bundled add-ons (such as Online Security or Backup) show markedly higher attrition rates.

---

## 🛠️ Tech Stack & Methods

* **Tool:** Microsoft Power BI Desktop
* **Data Transformation:** Power Query (ETL, schema cleanup, null management, categorical encoding)
* **Modeling:** Custom DAX measures, dynamic text formatting strings, switch-based segmentation logic
* **UI/UX:** Dark-mode interface (`#0c1527`), high-contrast categorical palette (Teal `#00D2BE` for Retained, Coral `#FF5C5C` for Churned), custom card layering, and custom visual padding.

---

## 📐 Key DAX Measures Used

### 1. Retention Rate %
```dax
Retention Rate % = 
VAR TotalCust = COUNTROWS('telco_churn_unclean')
VAR RetainedCust = 
    CALCULATE(
        COUNTROWS('telco_churn_unclean'), 
        'telco_churn_unclean'[Churn] = "No"
    )
RETURN
DIVIDE(RetainedCust, TotalCust, 0)
