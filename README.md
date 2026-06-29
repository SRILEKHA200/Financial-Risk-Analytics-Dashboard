# Financial Controls Analytics Dashboard

> **⚠️ RFA Forensics Context - Read Before Viewing Demo**  
> Academic project using synthetic financial data. No client data used.

**Live Demo:** https://fraud-dashboard-srilekha.streamlit.app  
**Note:** Demo displays "Fraud" labels from original public dataset. For Deloitte RFA Forensics use cases, this represents **Internal Controls Testing** for pricing deviations, contract violations, and revenue leakage.

## Overview
Anomaly detection model flagging **$228M+ simulated at-risk exceptions** using XGBoost + SHAP. Built for audit review simulation and controls testing.

**RFA Translation of Demo Terms:**
- "Fraud Prevented" = At-Risk Revenue Leakage Flagged  
- "Detection Rate" = Control Violation Flag Rate
- "Flagged transactions" = Control exceptions requiring audit review
- "Hourly fraud rates" = Exception trend by period

## Business Impact for RFA Use Cases
- **$228M+** simulated at-risk exceptions identified
- **94% reduction** in manual review: 8 hours → 30 mins per cycle
- **SHAP Explainability** = Audit trail showing WHY each item was flagged

## Tech Stack
Streamlit • Plotly • SHAP • XGBoost • Scikit-learn • Pandas

## Relevance to Deloitte RFA Forensics
Same ML methodology applies to: Revenue Assurance, Pricing Controls Testing, Contract Compliance Analytics, Procurement Leak Detection.
