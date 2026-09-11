# 📦 Supply Chain Delivery Performance & Profitability Analysis

Data-driven investigation into chronic late deliveries at a global e-commerce company, quantifying their financial impact and building a predictive model to flag at-risk orders before they ship.

---

## 🔎 Overview

This project analyzes **172,765 orders** placed between **January 2015 and January 2018** by a global e-commerce platform selling sporting goods, fitness equipment, outdoor gear, footwear, and apparel across multiple international regions.

The core business problem: actual shipping times routinely miss promised delivery windows, eroding customer trust, cutting into order profitability, and making it impossible to give buyers reliable delivery commitments at checkout.

**Headline finding:** 54.71% of all orders arrive late, putting **$2.1M** of profit at risk against a total profit base of **$7.5M**. A Random Forest model built on order-level features predicts late deliveries with **74% accuracy**.

---

## 🎯 Objectives

- Assess delivery performance across region, shipping mode, time, and customer segment
- Quantify how delays affect order-level profitability
- Pinpoint the operational bottlenecks driving lateness
- Build a predictive model to flag high-risk orders pre-shipment
- Translate findings into prioritized, actionable recommendations

---

## 📊 Key Metrics

| Metric | Value |
|---|---|
| Total Orders Analyzed | 172,765 |
| Late Deliveries | 94,523 |
| Late Delivery Rate | 54.71% |
| On-Time Delivery Rate | 45.29% |
| Total Profit (all orders) | $7.5M |
| Profit at Risk (delayed orders) | $2.1M |
| Average Delivery Delay | 3 days |
| Average Profit per Order | $22.03 |
| Predictive Model Accuracy | 74% |

---

## 🧩 Analysis Breakdown

### 1. Profitability Analysis
- 80.7% of orders are profitable; 18.7% are loss-making, disproportionately concentrated among delayed shipments
- 31.0% of orders arrive exactly 1 day late — the single largest delay cohort
- Mean profit per order stays flat (~$21–$23) regardless of delay length, indicating the profit problem is driven by **volume** of delayed orders, not the economics of any individual order

### 2. Bottleneck Detection
Delay rates were compared across six operational dimensions:

| Dimension | Finding |
|---|---|
| **Shipping Mode** | First Class: 100% delayed · Second Class: 79.8% · Standard Class: 39.8% · Same Day: 0% |
| **Region** | Tight spread (55–59%); Central Africa highest at 58.7% — rules out a localized failure |
| **Customer Segment** | Nearly identical across Consumer, Corporate, Home Office (54.5–55.4%) |
| **Department** | Health & Beauty (56.9%) and Pet Shop (56.6%) lead |

**Shipping mode is the single most impactful lever** for improving delivery performance.

### 3. Root Cause Analysis
Deep-dive on the highest-delay region (Central Africa, 58.7%) and department (Health & Beauty, 56.9%) surfaced recurring top drivers:
- First/Second Class shipping assignment
- Orders stuck in `PAYMENT_REVIEW` or `PENDING` status
- Category-specific effects in Outdoors and Golf (Central Africa)

### 4. Time-Based Patterns
- Delay rates are fairly stable over time (53–57% range)
- Peak delay months: **August, September (55.4%)**, and **December (55.2%)** — consistent with mid-year promotions and Q4 holiday demand
- **July** is the seasonal low point (~53.75%)
- Day-of-week variance is minimal (<1 pt spread)
- Intra-day peaks around **hour 21 (57.1%)** and midday (hours 11–12), suggesting cutoff and peak-volume bottlenecks

### 5. Machine Learning Model
A Random Forest classifier was trained to predict `Late_delivery_risk`:

- **Pipeline:** frequency encoding of categoricals → stratified train/test split → SMOTE oversampling for class balance → Random Forest classifier
- **Overall accuracy:** 74%
- **Late-order precision:** 0.78 · **Late-order recall:** 0.75
- **On-time precision:** 0.68 · **On-time recall:** 0.72

The model is precise enough to support targeted operational interventions (e.g., proactive customer alerts, priority handling) without excessive false alarms.

---

## ✅ Strategic Recommendations

| Priority | Recommendation |
|---|---|
| Critical | Audit First & Second Class shipping SLAs; consider suspending or repricing First Class |
| High | Deploy the Random Forest model as a production pilot for order-level risk alerts |
| High | Automate escalation for orders stuck in payment review/pending status |
| Medium | Build seasonal surge capacity plans for Aug, Oct, Dec peaks |
| Medium | Default eligible orders to Standard Class shipping |
| Medium | Audit Outdoors and Golf category fulfillment in Central Africa |
| Low | Review pricing/discount strategy behind the 18.7% loss-making orders |
| Low | Retrain the model quarterly; target >80% late-order recall within 6 months |

### Target Outcomes (12-month horizon)

| Area | Current | Target |
|---|---|---|
| Late Delivery Rate | 54.71% | < 30% |
| First Class On-Time Rate | 0% | > 80% |
| Second Class On-Time Rate | 20.2% | > 60% |
| Model Accuracy | 74% | > 82% |
| Loss-Making Orders | 18.7% | < 12% |
| Profit at Risk | $2.1M | Reduce by 40% |

---

## 🛠️ Tech Stack

> Update this section to match your actual implementation.

- **Language:** Python (pandas, numpy)
- **Modeling:** scikit-learn (Random Forest), imbalanced-learn (SMOTE)
- **Visualization:** matplotlib / seaborn / Plotly
- **Reporting:** Jupyter Notebook, exported PDF/DOCX report

---

## 📁 Repository Structure

```
├── data/                   # Raw and processed datasets
├── notebooks/              # EDA, bottleneck detection, root cause analysis, modeling
├── reports/                # Final report (PDF/DOCX) and supporting visuals
├── src/                    # Reusable scripts (data prep, feature engineering, model training)
├── requirements.txt        # Python dependencies
└── README.md
```

*(Adjust folder names to match your actual repo layout.)*

---

## 🚀 Getting Started

```bash
# Clone the repo
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# Install dependencies
pip install -r requirements.txt

# Run the analysis notebooks in order
jupyter notebook notebooks/
```

---

## 📄 Full Report

The complete write-up — including all charts, the KPI dashboard, and detailed root cause breakdowns — is available in [`reports/`](./reports).

---

## 👤 Author

**Akash Kumar Rakshit**
