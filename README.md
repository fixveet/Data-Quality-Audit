# 🛒 Amazon India E-Commerce — Data Quality Audit

> **38.7% of raw records were not analysis-ready.**
> Without validation, revenue appeared as **INR 78.6M**. After cleaning? **INR 67.0M**.
> That's a **14.7% overstatement** from unvalidated data.

This project audits an Amazon India e-commerce dataset to validate revenue integrity *before* performing business analysis because clean data is not optional.

---

## 📦 Dataset

| Attribute | Details |
|-----------|---------|
| **Source** | [Kaggle: Unlock Profits with E-Commerce Sales Data](https://www.kaggle.com/datasets/thedevastator/unlock-profits-with-e-commerce-sales-data) |
| **Period** | April 2022 transactions |
| **Records** | 128,975 |
| **Columns** | 24 |
| **Category** | Fashion orders |
| **Includes** | Order status, fulfillment type, quantity, revenue, B2B flag |

---

## ❓ Business Problem

Finance teams often receive raw transactional exports and use them directly for reporting. But what if:

- Cancelled orders are still counted as revenue?
- Duplicate order IDs inflate volume?
- Transactions have zero quantity or missing amounts?

**This project answers one critical question: Can the reported revenue actually be trusted?**

---

## ✅ Data Validation Rules

Six business validation rules were implemented:

| # | Rule | Issue Detected |
|---|------|----------------|
| 1 | `Qty ≤ 0` | Invalid transaction |
| 2 | `Amount` is null or 0 | Not financially valid |
| 3 | Missing SKU | Inventory inconsistency |
| 4 | Invalid / future dates | System error |
| 5 | Duplicate Order ID | Double-counted revenue |
| 6 | Cancelled orders | Should not be recognized as revenue |

---

## 🔍 Key Findings

```
Raw Records:       128,975
Problematic:        49,874  (38.7%)
Valid Records:     100,727
```

### Revenue Impact

| Metric | Value |
|--------|-------|
| Raw Revenue | INR 78.6M |
| Valid Revenue | INR 67.0M |
| **Overstatement** | **INR 11.6M (14.7%)** |

### Root Causes of Overstatement

- **18,332** cancelled orders included in revenue
- **7,344** duplicate order IDs inflating volume
- Remaining: null/invalid quantity & amount records

---

## 📊 Operational Insights

### Cancellation Rate by Fulfillment Type

| Fulfillment | Cancellation Rate |
|-------------|-------------------|
| Merchant | 17.5% |
| Amazon | 12.8% |
| **Gap** | **4.7%** |

### Revenue Concentration

| Category | Revenue Share |
|----------|---------------|
| Set | 50.0% |
| Kurta | 26.7% |
| **Combined** | **76.7%** |

> ⚠️ High revenue dependency on just two categories represents significant concentration risk.

### B2B Segment

- Only **0.8%** revenue share
- **Higher Average Order Value** than consumer segment
- Represents an **untapped growth opportunity**

---

## 🧹 Data Cleaning Process

1. Remove export artefact column
2. Filter out cancelled orders
3. Remove invalid quantity records (`Qty ≤ 0`)
4. Remove null/zero amount records
5. Deduplicate by Order ID

**Result:** 100,727 valid, analysis-ready transactions

---

## 🛠️ Tools Used

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

---

## 📁 Project Structure

```
├── amazon_data_quality_audit.ipynb   # Full audit notebook
├── amazon_audit_report.pdf           # Summary report
└── README.md                         # This file
```

---

## 🏁 Conclusion

**Clean data is not optional.**

Without validation, revenue was overstated by **14.7%**. Data quality directly impacts financial reporting, operational performance evaluation, and strategic decisions.

> *Before analyzing performance, validate the foundation.*
