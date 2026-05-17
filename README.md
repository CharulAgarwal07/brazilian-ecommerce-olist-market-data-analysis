# 🛒 Olist Brazilian E-Commerce — Customer Behaviour & Retention Analysis

> Data Analyst Case Study · Habuild · Dataset: [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

---

## Overview

This project analyses ~100,000 real orders from Olist — a large Brazilian e-commerce marketplace — spanning **September 2016 to August 2018**. The goal was to surface customer behaviour patterns, test delivery and satisfaction hypotheses, and identify actionable growth levers for a marketing team.

The analysis covers:
- Exploratory data analysis across 9 relational tables
- Customer retention and cohort behaviour
- Geographic delivery performance
- Product category profitability vs satisfaction
- Statistical hypothesis testing (Mann-Whitney U, Spearman correlation)
- Two actionable recommendations backed by data

---

## Key Findings

| Finding | Detail |
|---|---|
| 📈 Platform growth | 23× order volume increase in 24 months (300 → 7,000 orders/month) |
| 😶 Retention crisis | **96.9% of customers ordered only once** — all revenue growth is acquisition-driven |
| 🚚 Late = 1-star | Late deliveries cause 1-star rate to jump from 7% → 49% (p < 0.0001) |
| 📍 SP advantage | São Paulo customers get orders in **7 days median** vs 14 days nationally |
| ⭐ Category winner | Health & beauty: top revenue + top satisfaction — the standout category |
| ⏱️ 12-day threshold | Review scores stay above 4.2 within 12 days of delivery, then fall sharply |

---

## Project Structure

```
olist-analysis/
│
├── olist_analysis.ipynb          # Main analysis notebook
│
├── data/                         # Place Kaggle CSVs here (not committed)
│   ├── olist_customers_dataset.csv
│   ├── olist_orders_dataset.csv
│   ├── olist_order_items_dataset.csv
│   ├── olist_products_dataset.csv
│   ├── olist_order_reviews_dataset.csv
│   ├── olist_order_payments_dataset.csv
│   ├── olist_sellers_dataset.csv
│   ├── olist_geolocation_dataset.csv
│   └── product_category_name_translation.csv
│
├── plots/                        # All generated charts (auto-saved by notebook)
│   ├── plot_01_monthly_orders_revenue.png
│   ├── plot_02_hour_weekday.png
│   ├── plot_03_categories.png
│   ├── plot_04_geo.png
│   ├── plot_05_payment.png
│   ├── plot_06_reviews.png
│   ├── plot_07_retention.png
│   ├── plot_08_value_delivery_review.png
│   ├── plot_09_h1_late_vs_review.png
│   ├── plot_10_h2_sp_delivery.png
│   ├── plot_11_h3_installments_review.png
│   ├── plot_12_seller_pareto.png
│   └── plot_13_delivery_window.png
│
└── Habuild_Report_Final.docx     # 5-page summary report
```

---

## Setup & Usage

### 1. Clone the repo
```bash
https://github.com/CharulAgarwal07/brazilian-ecommerce-olist-market-data-analysis.git
cd brazilian-ecommerce-olist-market-data-analysis
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scipy
```

### 3. Download the dataset
Get the data from [Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce), extract all CSVs into the `data/` folder.

### 4. Run the notebook
```bash
jupyter notebook olist_analysis.ipynb
```

Run all cells top-to-bottom. Charts will be auto-saved as `.png` files in your working directory.

---

## Analysis Walkthrough

### Data Model

The dataset is multi-table and relational. All 9 tables were merged into a single master dataframe:

```
customers ──┐
orders ──────┼── master dataframe
items ───────┤   (+ derived cols: delivery_days, delay_days,
products ────┤    is_late, weekday, hour, cohort_month)
reviews ─────┤
payments ────┘
```

Derived variables computed per order:
- `delivery_days` — actual time from purchase to delivery
- `delay_days` — actual minus estimated delivery (positive = late)
- `is_late` — boolean flag for late orders
- `cohort_month` — customer's first purchase month

---

### EDA Highlights

**Monthly growth**

Orders grew 23× in 24 months. Revenue tracked volume linearly — average order value (~BRL 154) stayed stable throughout. A clear Black Friday spike in November 2017 is visible in both orders and revenue.

**Shopping behaviour**

Orders peak between 10am–4pm on weekdays. Saturday is the weakest day (~31% below Monday). This has a direct implication for when marketing campaigns should be scheduled.

**Category performance**

Health & beauty is the strongest category — top-quartile revenue and highest average review score (~4.4). Bed/bath/table leads in volume but has the lowest satisfaction score (~4.0) among the top 15. Telephony and furniture underperform on satisfaction, likely due to delivery difficulty with large/bulky items.

**Geographic delivery gap**

São Paulo (SP) accounts for 40%+ of orders and delivers in a median of 7 days. Northeast states — Alagoas (AL), Maranhão (MA), Sergipe (SE) — show late delivery rates of 15–20% and delivery windows of 20–30 days. Customers in these states are having a fundamentally different (worse) experience.

**Non-intuitive finding — 96.9% of customers never return**

Despite 23× revenue growth, 96.9% of customers placed exactly one order. The cohort chart shows repeat rates declining from ~7.5% for early cohorts (Jan 2017) to below 1% for 2018 cohorts. All revenue growth is acquisition-driven — there is essentially no organic retention engine.

---

### Hypotheses Tested

#### H1 — Late delivery causes significantly lower review scores

```
H₀: No difference in review scores between late and on-time orders
H₁: Late orders receive lower scores (one-tailed)
Test: Mann-Whitney U (ordinal data, non-normal distribution)
```

| Group | Avg Review |
|---|---|
| On-time | 4.28 |
| Late | 2.55 |

**p-value: < 0.0001 → Reject H₀**

Late delivery increases the 1-star rate from 7% to 49% and drops the 5-star rate from 62% to 20%. The strongest single controllable predictor of satisfaction in the dataset.

---

#### H2 — SP customers receive faster deliveries than the rest of Brazil

```
H₀: SP delivery time = national median
H₁: SP customers get faster delivery (one-tailed)
Test: Mann-Whitney U
```

| Group | Median Delivery |
|---|---|
| SP | 7 days |
| Non-SP | 14 days |

**p-value: < 0.0001 → Reject H₀**

SP's entire IQR sits below the national median. The gap is structural — seller concentration in SP creates a first-mile speed advantage that remote states simply don't get.

---

#### H3 (Bonus) — More instalments correlate with lower satisfaction

```
H₀: No correlation between instalment count and review score
H₁: Negative correlation (Spearman rank)
```

| Spearman rho | p-value |
|---|---|
| -0.024 | < 0.0001 |

**Technically confirmed, practically unimportant.** The effect size is negligible — review scores are flat across 1–9 instalments. Only a minor dip appears at 10–11 instalments. Delivery time, not payment method, is the dominant satisfaction driver.

---

### Actionables

**1 — Post-purchase retention campaign**

Trigger a personalised email 7–10 days after first delivery with category recommendations and a first-repeat-purchase discount (10% off or free shipping, 30-day validity). Segment by review score: 4–5 star customers first, then service recovery messages for 1–2 star customers before any promo.

Rough estimate: lifting repeat rate from 3.1% → 8% on a 5,000-order monthly cohort adds ~BRL 53,000/month in incremental revenue at near-zero acquisition cost.

**2 — Delivery SLA fix for high-late-rate states**

The top 16% of sellers drive 80% of all orders (Pareto curve in notebook). Work with this concentrated group to pre-position inventory closer to northeast customers. Negotiate carrier SLA penalties for AL, MA, SE routes. Set state-specific delivery date estimates on product pages anchored to achievable windows — not the SP-calibrated default.

---

### Further Exploration

**Is late delivery driven by a concentrated set of sellers or carriers?**

This analysis proves that late delivery destroys satisfaction but doesn't identify *where* the delay originates. If 20% of sellers cause 80% of delays, a targeted quality programme would be far more efficient than broad logistics changes.

Proposed: join `order_items → sellers`, compute per-seller late delivery rates, build a Pareto curve for delay contribution, then apply a logistic regression with features: `seller_id`, `customer_state`, `product_weight_g`, and carrier. All required tables are in the dataset but the carrier-level join was not completed in this analysis.

---

## Tech Stack

| Tool | Use |
|---|---|
| Python 3.9+ | Core analysis |
| pandas | Data loading, merging, derived columns |
| matplotlib / seaborn | All visualisations |
| scipy.stats | Mann-Whitney U and Spearman correlation tests |
| Jupyter Notebook | Analysis environment |

---

## LLM Disclosure

Per the Habuild case study guidelines:

**Claude Sonnet 4 (Anthropic) was used for:**
- Python/pandas syntax (cells 1–4)
- matplotlib/seaborn chart formatting (cells 5–13)
- scipy.stats import syntax for statistical tests (cells 14–16)
- docx-js JavaScript syntax for generating the Word report

**Claude was NOT used for:**
- Hypotheses (independently identified from EDA output)
- Analytical observations and interpretations
- Business recommendations
- The non-intuitive retention finding
- Further exploration framing

---

## Dataset

**Source:** [Olist Brazilian E-Commerce Public Dataset — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

9 tables, ~100k orders, Sep 2016 – Aug 2018. Data is publicly available under a CC BY-NC-SA 4.0 license. Not committed to this repo — download directly from Kaggle and place CSVs in `data/`.

---

## License

MIT — feel free to use or adapt for your own analysis.

# Author

Charul Agarwal

GitHub: https://github.com/CharulAgarwal07/
LinkedIn: https://www.linkedin.com/in/charul-agarwal-b4823a281/
