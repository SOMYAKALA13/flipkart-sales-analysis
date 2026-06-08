# 🛒 Flipkart Sales Analysis

A complete end-to-end data analysis project on Flipkart e-commerce sales data using **Python**, **MySQL**, and **Power BI**.

---

## 📌 Project Overview

This project analyzes 1,000 Flipkart sales orders to uncover insights around revenue trends, product performance, customer behavior, and regional sales patterns. The analysis spans three tools — Python for data cleaning and EDA, MySQL for structured querying, and Power BI for interactive visualization.

---

## 🗂️ Dataset

| Column | Description |
|--------|-------------|
| Order ID | Unique identifier for each order |
| Product Name | Name of the product sold |
| Category | Product category (Electronics, Clothing, Books, Beauty, Home & Kitchen) |
| Price (INR) | Unit price of the product |
| Quantity Sold | Number of units sold |
| Total Sales (INR) | Revenue generated per order |
| Order Date | Date of the order |
| Payment Method | Mode of payment (UPI, Wallet, Debit Card, COD, Net Banking, Credit Card) |
| Customer Rating | Rating given by customer (1–5) |
| Month | Month of the order |
| Year | Year of the order |
| Profit (INR) | Profit earned per order |
| Discount % | Discount applied on the product |
| Customer Segment | Segment of the customer (Online, Retail, Wholesale) |
| Region | Geographic region (North, South, East, West) |

- **Total Records:** 1,000 rows
- **Time Period:** 2024–2025

---

## 🛠️ Tools & Technologies

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![MySQL](https://img.shields.io/badge/MySQL-8.0-orange?logo=mysql)
![Power BI](https://img.shields.io/badge/PowerBI-Dashboard-yellow?logo=powerbi)
![Pandas](https://img.shields.io/badge/Pandas-EDA-lightblue?logo=pandas)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-green)

---

## 🐍 Python — Data Cleaning & EDA

### Steps Performed
- Loaded dataset using `pandas`
- Checked shape, dtypes, null values using `df.info()`, `df.describe()`, `df.isnull().sum()`
- Converted `Order Date` to datetime using `pd.to_datetime()`
- Extracted `day` column from Order Date using `.dt.day_name()`
- Standardized column names to uppercase using `.str.upper()`
- Exported cleaned data to CSV for Power BI and MySQL

### Key Analyses
- **Revenue by Category** — Electronics leads with ₹1.73 Cr
- **Sales by Month** — July shows peak sales
- **Average Rating by Customer Segment** — Online customers rate highest (3.07)

### Files
```
flipkart_eda.ipynb       # Jupyter notebook with full EDA
flipkart_cleaned.csv     # Cleaned dataset
```

---

## 🗄️ MySQL — Business Queries

Connected cleaned dataset to MySQL (`flipkart_db`) and ran structured queries:

| Query | Insight |
|-------|---------|
| Total Orders | 1,000 orders |
| Total Revenue | ₹75.21M |
| Avg Customer Rating | 3.01 |
| Revenue by Category | Electronics > Clothing > Books > Beauty > Home & Kitchen |
| Top 10 Products by Revenue | Smartwatch, Table Lamp top performers |
| Most Preferred Payment Method | UPI is #1 |
| Monthly Revenue | Sorted by highest revenue month |
| Avg Discount by Category | Compared across all 5 categories |
| Top Product per Category | Using `RANK()` window function |
| Region Ranking by Revenue | Using `RANK()` window function |

### SQL Highlights
```sql
-- Top Product in Each Category using Window Function
SELECT * FROM (
    SELECT CATEGORY, `PRODUCT NAME`,
           SUM(`TOTAL SALES (INR)`) AS REVENUE,
           RANK() OVER(PARTITION BY CATEGORY ORDER BY SUM(`TOTAL SALES (INR)`) DESC) AS RNK
    FROM flipkart_cleaned
    GROUP BY CATEGORY, `PRODUCT NAME`
) X
WHERE RNK = 1;

-- Rank Regions by Revenue
SELECT REGION, SUM(`TOTAL SALES (INR)`) AS TOTAL_REVENUE,
       RANK() OVER(ORDER BY SUM(`TOTAL SALES (INR)`) DESC) AS REGION_RNK
FROM flipkart_cleaned
GROUP BY REGION;
```

---

## 📊 Power BI — Interactive Dashboard

### KPI Cards
- Total Revenue: **₹75.21M**
- Total Orders: **1K**
- Avg Rating: **3.01**
- Avg Order Value: **₹75.21K**
- Qty Sold: **3K**

### Visuals Built
- 📈 Total Revenue by Month (Line Chart) — sorted Jan→Dec
- 🍩 Count by Region (Donut Chart)
- 📊 Quantity Sold by Category (Bar Chart)
- 💳 Total Orders by Payment Method (Bar Chart)
- 💰 Profit by Product (Bar Chart)

### Dashboard Preview
> *Screenshot of Power BI dashboard included in `/assets` folder*

---

## 💡 Key Business Insights

1. **Electronics is the top revenue-generating category** — ₹1.73 Cr out of ₹7.52 Cr total
2. **UPI is the most preferred payment method** — reflects India's digital payment trend
3. **July records the highest monthly sales** — potential seasonal demand spike
4. **Online customer segment gives the highest ratings** — better satisfaction than Retail/Wholesale
5. **Revenue is evenly distributed across regions** — North (26.9%), South (25.9%), East (24.6%), West (22.6%)

---

## 📁 Project Structure

```
flipkart-sales-analysis/
│
├── data/
│   └── flipkart_cleaned.csv
│
├── python/
│   └── flipkart_eda.ipynb
│
├── sql/
│   └── flipkart_queries.sql
│
├── assets/
│   └── dashboard_screenshot.png
│
└── README.md
```

---

## 🚀 How to Run

### Python
```bash
pip install pandas matplotlib
jupyter notebook flipkart_eda.ipynb
```

### MySQL
```sql
CREATE DATABASE flipkart_db;
USE flipkart_db;
-- Import flipkart_cleaned.csv as table
-- Run queries from flipkart_queries.sql
```

### Power BI
- Open `.pbix` file in Power BI Desktop
- Data source: `flipkart_cleaned.csv`

---

## 👩‍💻 Author

**Somya Kala**  
B.Tech CSE — Graphic Era Hill University, Dehradun  
📧 [LinkedIn](https://linkedin.com/in/somya-kala-235b99220/) | 💻 [GitHub](https://github.com/SOMYAKALA13)
