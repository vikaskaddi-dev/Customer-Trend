# Customer-Trend
End-to-end customer shopping behavior analysis — Python data cleaning, SQL Server queries with window functions, and an interactive Power BI dashboard.

# Customer Shopping Behavior Analysis

An end-to-end data analytics project analyzing a 3,900-row retail customer shopping dataset — from raw data to an interactive dashboard — using Python, SQL Server, and Power BI.

## The Data

`customer_shopping_behavior.csv` — 3,900 customer transactions with 18 fields: Customer ID, Age, Gender, Item Purchased, Category, Purchase Amount, Location, Size, Color, Season, Review Rating, Subscription Status, Shipping Type, Discount Applied, Promo Code Used, Previous Purchases, Payment Method, and Frequency of Purchases.

## What I Did

**Data Cleaning & Feature Engineering (Python/Pandas):**
- Inspected the data (`.info()`, `.describe()`, null check) and found 37 missing values in Review Rating
- Filled missing ratings using **category-based imputation** — each missing rating filled with the median rating for that product's category, rather than a single global average
- Standardized column names to snake_case for consistency across tools
- Engineered an `age_group` feature, bucketing customers into Young Adult / Adult / Middle-aged / Senior using quartile-based binning (`pd.qcut`)

**SQL Analysis (SQL Server via SQLAlchemy/pyodbc):**
Loaded the cleaned data into a local SQL Server database and answered 10 business questions, including:
- Revenue by gender and by age group
- Customers who used a discount but still spent above the average
- Top 5 highest-rated products
- Standard vs. Express shipping spend comparison
- Subscriber vs. non-subscriber spending behavior
- Customer segmentation (New / Returning / Loyal) using a CTE
- **Top 3 best-selling products per category**, using the `ROW_NUMBER()` window function partitioned by category
- Whether repeat buyers (5+ previous purchases) are more likely to subscribe

**Dashboard (Power BI):**
Built an interactive dashboard (`Customer_behavior_dashboard.pbix`) surfacing the above findings visually — revenue breakdowns, subscription status, and category-level trends.

## Key Findings

- Missing review ratings were filled category-by-category rather than with one blanket average, preserving each category's rating pattern
- Products vary meaningfully in both average rating and discount usage — the top-rated products aren't necessarily the most discounted ones
- Customer segments (New / Returning / Loyal) show clearly different purchase volumes, useful for targeting retention efforts
- Window functions (`ROW_NUMBER() OVER (PARTITION BY ...)`) made "top N per group" questions (like top 3 products per category) straightforward — something a plain `GROUP BY` can't do alone

## Tools

Python (Pandas) · SQL Server (T-SQL, window functions, CTEs) · Power BI · SQLAlchemy/pyodbc

## Files

| File | Description |
|---|---|
| `customer_shopping_behavior.csv` | Raw dataset |
| `customer_shopping_behavior_analysis.ipynb` | Data cleaning and feature engineering notebook |
| `customer_behavior_sql_queries.sql` | 10 SQL queries answering specific business questions, including window functions and CTEs |
| `Customer_behavior_dashboard.pbix` | Interactive Power BI dashboard |

## How to Open

- **Notebook:** open in VS Code (with Jupyter extension), Google Colab, or Jupyter Notebook/Lab
- **SQL file:** written for SQL Server (T-SQL syntax) — open and run in SQL Server Management Studio (SSMS) against a database containing the cleaned `customer` table
- **Power BI file:** requires [Power BI Desktop](https://powerbi.microsoft.com/desktop) (free)
