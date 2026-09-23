# Walmart Sales Data Pipeline & Analysis

An end-to-end data project that takes raw Walmart transaction data, cleans and transforms it with **Python (pandas)**, loads it into **PostgreSQL**, and analyzes it to uncover revenue, profit, and customer behavior patterns across **100 branches and 5 years of sales**.

---

## Project Overview

Raw retail data is rarely analysis-ready. This dataset had duplicate invoices, missing values, prices stored as text (`"$74.69"`), and dates in `dd/mm/yy` format. This project builds a repeatable pipeline that fixes those issues, creates the metrics the business cares about (revenue and profit), and answers key questions about **what sells, when it sells, and how customers pay**.

**Business questions answered**

1. Which product categories drive the most revenue and profit?
2. When do customers shop: which months, days, and hours?
3. How do customers pay, and does payment method relate to order value?
4. Which branches and cities perform best?
5. Do customer ratings relate to category or order size?

---

## Dataset

| Property | Detail |
|---|---|
| File | `Walmart.csv` |
| Raw records | 10,051 rows |
| Clean records | **9,969 transactions** |
| Period | 1 Jan 2019 to 31 Dec 2023 |
| Coverage | 100 branches across 98 cities |
| Categories | 6 |

| Column | Description |
|---|---|
| `invoice_id` | Transaction ID |
| `Branch` | Branch code (e.g. WALM003) |
| `City` | City of the branch |
| `category` | Product category |
| `unit_price` | Price per unit (text with `$` in the raw file) |
| `quantity` | Units purchased |
| `date`, `time` | Transaction date (`dd/mm/yy`) and time |
| `payment_method` | Cash, Credit card, or Ewallet |
| `rating` | Customer rating (3 to 10) |
| `profit_margin` | Profit margin on the sale |

---

## ⚙️ Pipeline Steps

```
Walmart.csv  →  Extract  →  Clean  →  Transform  →  Load (PostgreSQL)  →  Analyze
```

**1. Extract:** Read the raw CSV into pandas.

**2. Clean**
- Removed **51 duplicate rows** (invoice IDs 9950–10000 appeared twice), leaving 10,000
- Dropped **31 rows** missing both `unit_price` and `quantity`, leaving 9,969
- Converted `unit_price` from text (`"$74.69"`) to a numeric type
- Parsed `date` from `dd/mm/yy` into a proper date and `time` into hours

**3. Transform (engineered columns)**

| Column | Formula |
|---|---|
| `revenue` | `unit_price × quantity` |
| `profit` | `revenue × profit_margin` |
| `hour`, `month`, `year`, `weekday` | Extracted from date and time |

**4. Load:** Wrote the cleaned table to a PostgreSQL database with SQLAlchemy.

**5. Analyze:** Aggregated in SQL and pandas, then summarized the findings below.

---

## Key Findings

**Total revenue: $1,209,726 · Total profit: $476,139 · Profit margin: 39.4% · Average order: $121.35 · Average rating: 5.83 / 10**

1. **Two categories carry the business.** Fashion accessories and Home and lifestyle make up **91% of transactions and 81% of revenue** (about $489K each).
2. **Small categories, big tickets.** Food and beverages, Sports and travel, and Health and beauty are only **5% of transactions but 12.6% of revenue**. Their average order is **~$311**, nearly triple the ~$108 of the two big categories, and they are rated higher (**7.0 vs 5.8**).
3. **Nov–Dec is the peak.** In every full year (2020–2023), November and December account for **~55% of annual revenue and transactions**. Order value stays flat, so the spike is customer volume, not higher spending.
4. **Evenings are the busiest.** Between **3 pm and 9 pm**, the business handles **64% of transactions and 62% of revenue**.
5. **Credit card and e-wallet lead, but cash orders are the largest.** Credit card is 40% of revenue and Ewallet 38%, while cash is 22%. Cash orders average **$143.88**, versus $115–118 for cards and e-wallets.
6. **Profit margin is steady at 39–40% across categories.** Profit follows revenue, so growth comes from selling more, not from a higher-margin category mix.
7. **Top locations:** Weslaco is the highest-revenue city ($46,352), followed by Waxahachie ($40,703). The top single branch is WALM009 ($25,688).
8. **Ratings barely track order value** (correlation of 0.11), and the two highest-volume categories have the lowest ratings.

---

## Recommendations

- **Prepare for Nov–Dec and the 3–9 pm window.** Concentrate staffing, stock, and promotions where more than half the year's revenue is earned.
- **Grow high-ticket categories.** Food and beverages, Sports and travel, and Health and beauty deliver ~3x the order value with better customer ratings, so cross-selling them into the two big categories is a clear opportunity.
- **Investigate the lower ratings** in Fashion accessories and Home and lifestyle, since they are 91% of transactions.
- **Review cash handling and pricing**, since cash customers spend the most per order.

---

## Data Notes

- **2019 only covers January to March.** There are no April–December 2019 records, so 2019 should not be compared with later full years. Year-over-year comparisons here use 2020–2023.
- `rating` ranges from 3 to 10 with no values below 3.
- The raw dataset appears to be a sample, so findings describe this data and may not generalize to Walmart overall.

---

##Tools & Skills

- **Python:** pandas, NumPy, Matplotlib
- **ETL design, data cleaning, and feature engineering**
- **Business analysis and storytelling** with data

---

## Suggested Repository Structure

```
walmart-sales-pipeline/
├── data/
│   └── Walmart.csv
├── notebooks/
│   └── walmart_analysis.ipynb
├── sql/
│   └── analysis_queries.sql
├── images/
└── README.md
```

*Adjust this to match your repo.*



Data Analyst · [GitHub @ChidinmaIwundu](https://github.com/ChidinmaIwundu)

*If you found this project useful, feel free to ⭐ the repo.*
