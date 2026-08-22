Walmart Sales Analysis

Exploratory and SQL-driven analysis of Walmart transaction data across 100 branches, aimed at uncovering sales trends, category performance, and profitability patterns to support data-driven retail decisions.


Business Problem

Retail chains generate large volumes of transactional data, but raw records rarely translate into action on their own. This project explores Walmart's sales data to answer:

Which product categories and branches drive the most revenue and profit?
How do sales vary by payment method, time of day, and season?
What's the relationship between pricing, quantity sold, and profit margin?
Are there data quality issues (missing values, inconsistent formats) that need cleaning before analysis?

Tools & Tech Stack
VS Code - Data exploration
Jupyter Notebook - data cleaning and exploratory analysis
Python (pandas, NumPy) — data cleaning and exploratory analysis
PostgreSQL — structured querying, aggregation, and window functions

Workflow
Ingestion — load CSV into pandas / PostgreSQL
Cleaning — strip $ from unit_price, parse date as DD/MM/YY, handle missing unit_price/quantity rows with python
Transformation — derive revenue (unit_price × quantity), extract year, month, day_of_week, hour from date/time
Analysis — SQL/pandas queries to calculate:
Revenue and profit by category, branch, and city
Sales trends by month/year and time of day
Payment method distribution and average transaction value
Correlation between rating and profit margin
