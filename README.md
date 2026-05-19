# Fraud Detection Dashboard

**Live Demo:** https://fraud-dashboard-srilekha.streamlit.app

## Overview
End-to-end fraud detection system with ML model, SHAP explainability, and interactive Streamlit dashboard.

## Features
- **Multi-page Streamlit app**: Overview, Investigate, Explain
- **Business Impact metrics**: Fraud prevented, Detection rate, False positives
- **Interactive Plotly charts**: Risk tiers, hourly fraud rates
- **SHAP explainability**: Waterfall plots for individual transaction decisions
- **Case management**: Search, filter, and investigate flagged transactions

## Tech Stack
Streamlit • Plotly • SHAP • XGBoost • Scikit-learn • Pandas

## Run Locally
```bash
pip install -r requirements.txt
streamlit run app.py
   
   ## Task 8 — Insights & Business Recommendations
   
   #### 1. Which model performed best and why?
   **XGBoost** performed best based on PR-AUC.
   - **PR-AUC**: XGBoost = **0.626** vs LightGBM = **0.543**
   - **Reason**: XGBoost has higher PR-AUC, meaning better precision-recall tradeoff across all thresholds. At default threshold, XGBoost also had higher precision **0.781** and recall **0.492** vs LightGBM's **0.718** and **0.431**.
   
   #### 2. Why PR-AUC matters more than accuracy in fraud detection?
   Your dataset: **168 fraud cases / 5,000 transactions = 3.36% fraud rate**. Both models show **>97% accuracy** which looks great but is misleading. 
   **PR-AUC measures performance on fraud cases only**. XGBoost's **0.626 PR-AUC** vs LightGBM's **0.543** tells us XGBoost ranks fraud cases higher. Your dashboard's **83.7% precision + 64.3% recall** at threshold **0.417** proves real fraud-catching ability that accuracy hides.
   
   #### 3. Top 3 fraud signals identified by SHAP
   From your SHAP Global Summary Plot:
   1. **`card2`** - Strongest impact on fraud probability
   2. **`card4`** - High values push predictions toward fraud  
   3. **`D1`** - Third most important feature with clear separation
   
   #### 4. Common characteristics of Critical Risk transactions
   1. **Probability**: Model score >**0.417**, with dashboard showing **83.7% precision** at that threshold
   2. **Amount**: Avg fraud transaction is **$1.36**, indicating card-testing behavior
   3. **Card patterns**: Extreme values in `card2` and `card4` fields
   4. **Recall impact**: At **0.417** threshold, we catch **64.3%** of all fraud cases
   
   #### 5. Two actionable fraud prevention policies
   1. **Threshold-based auto-hold**: Hold any transaction with probability >**0.417** for manual review. At **83.7% precision**, 5 out of 6 flagged transactions are real fraud.
   2. **Micro-transaction + card rule**: Flag transactions <$5 if `card2` or `card4` are in high-risk ranges from SHAP. Targets the **$1.36** avg fraud pattern.
   
   #### 6. Estimated money saved annually
   **Using your actual numbers:**
   - Dataset: **168 fraud / 5,000 txns**
   - Recall at **0.417**: **64.3%** → **108 fraud cases caught**
   - Avg fraud loss: **$1.36**
   - **Sample savings: 108 × $1.36 = $146.88**
   
   **Scaled to 1M transactions/year**:
   Cases caught = 108/5000 × 1,000,000 = **21,600**  
   **Gross savings = 21,600 × $1.36 = $29,376/year**  
   FP review cost: 60 × $15 = **$900**  
   **Net estimated savings ≈ $28,476/year**
   
   #### 7. Model limitations
   1. **Low PR-AUC**: **0.626** for XGBoost means there's still major room for improvement. 35.7% of fraud is missed at **0.417** threshold.
   2. **Low dollar impact**: **$1.36** avg fraud means individual misses don't hurt much, but volume and reputation damage matter.
   3. **Anonymized features**: `card2`, `card4`, `D1` give no business meaning for rule creation.
   
   #### 8. Additional data that could improve performance
   1. **Real card features**: BIN, issuer country, card type to replace anonymized `card2`/`card4` and boost PR-AUC above **0.626**
   2. **Velocity features**: Transaction count per card/email in last 1hr to catch card testing
   3. **Device fingerprint**: Link the $1.36 tests to later large frauds from same device
