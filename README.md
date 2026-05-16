# brazilian-ecommerce-olist-market-data-analysis

# Olist E-Commerce Data Analysis

## Overview

This project presents a complete exploratory data analysis and statistical investigation of the Brazilian Olist e-commerce dataset.

The analysis focuses on:

- Customer retention
- Delivery performance
- Review score drivers
- Geographic inequality
- Payment behavior
- Revenue and category trends

The project includes:

- Data cleaning
- Feature engineering
- Multi-table joins
- Statistical hypothesis testing
- Business recommendations

---

# Dataset

Dataset: Brazilian E-Commerce Public Dataset by Olist

Source:  
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Time Period:
Sep 2016 – Aug 2018

Dataset Size:
~100,000 orders

---

# Tech Stack

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Jupyter Notebook

---

# Project Structure

```text
olist-analysis/
│
├── olist_analysis.ipynb
├── Habuild_Olist_Report.pdf
├── README.md
├── requirements.txt
│
├── plots/
│   ├── plot_01_monthly_trends.png
│   ├── plot_02_orders_by_hour.png
│   ├── plot_03_categories.png
│   ├── plot_04_geography.png
│   ├── plot_05_payments.png
│   ├── plot_06_reviews.png
│   ├── plot_07_retention.png
│   ├── plot_08_delivery_vs_review.png
│   ├── plot_09_delivery_threshold.png
│   ├── plot_10_h1_late_reviews.png
│   ├── plot_11_h3_installments_review.png
│
└── data/   (excluded from GitHub)
```

---

# Key Insights

## 1. Extremely Low Customer Retention

96.9% of customers placed only one order.

Despite rapid revenue growth, the platform relies almost entirely on continuous customer acquisition.

### Retention Distribution

![Retention Analysis](plots/plot_07_retention.png)

---

## 2. Delivery Delays Strongly Reduce Review Scores

Late deliveries dramatically increase 1-star reviews and reduce 5-star reviews.

### Late vs On-Time Review Distribution

![Late Delivery Impact](plots/plot_10_h1_late_reviews.png)

---

## 3. São Paulo Has Major Logistics Advantage

São Paulo customers receive deliveries significantly faster than the national median.

### Geographic Delivery Performance

![Geographic Analysis](plots/plot_04_geography.png)

---

## 4. Delivery Time Has a Critical Threshold

Review scores remain relatively stable until delivery exceeds ~12 days.

After that point, satisfaction drops sharply.

### Delivery Threshold Effect

![Delivery Threshold](plots/plot_09_delivery_threshold.png)

---

# Hypothesis Testing

## H1 — Late Delivery Reduces Review Scores

- Test: Mann–Whitney U
- Result: Statistically significant
- p-value < 0.0001

Conclusion:
Late delivery is the strongest controllable driver of customer dissatisfaction.

---

## H2 — São Paulo Receives Faster Deliveries

- Test: Mann–Whitney U
- Result: Significant difference found
- p-value < 0.0001

Conclusion:
Geographic inequality creates inconsistent customer experiences.

---

## H3 — More Installments Lower Review Scores

- Test: Spearman Correlation
- Result: Weak negative relationship
- Practical impact negligible

### Installments vs Review Score

![Installments Analysis](plots/plot_11_h3_installments_review.png)

---

# Business Recommendations

## Improve Customer Retention

- Personalized post-purchase campaigns
- Repeat-purchase incentives
- Category-based recommendations
- Win-back campaigns for first-time buyers

---

## Improve Delivery SLAs

Focus logistics improvements in:

- AL
- MA
- SE
- PI

These states showed the highest late-delivery rates.

---

## Seller-Level Logistics Monitoring

Identify sellers contributing disproportionately to delays and establish stricter delivery SLAs.

---

# Visualizations

## Monthly Growth Trends

![Monthly Trends](plots/plot_01_monthly_trends.png)

---

## Shopping Behavior by Time

![Shopping Behavior](plots/plot_02_orders_by_hour.png)

---

## Product Category Analysis

![Category Analysis](plots/plot_03_categories.png)

---

# How to Run

## 1. Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/olist-analysis.git
```

## 2. Install Dependencies

```bash
pip install -r requirements.txt
```

## 3. Open Notebook

```bash
jupyter notebook
```

Open:

```text
olist_analysis.ipynb
```

Run all cells sequentially.

---

# Results

The notebook generates:

- Clean master analysis dataset
- Statistical test outputs
- Business visualizations
- PNG plot exports

---

# Learning Outcomes

This project improved skills in:

- Data cleaning
- Exploratory data analysis
- Statistical testing
- Data visualization
- Business storytelling
- Customer analytics

---

# LLM Usage Disclosure

LLM assistance was used for:

- Python syntax support
- Debugging
- Visualization guidance

All findings, interpretations, business insights, and recommendations were independently reviewed and written.

---

# Author

Charul Agarwal

GitHub: https://github.com/YOUR_USERNAME  
LinkedIn: Add LinkedIn URL
