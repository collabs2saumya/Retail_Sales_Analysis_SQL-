# Retail_Sales_Analysis_SQL-
# Retail Sales Analysis – README.md

````markdown
# 🛒 Retail Sales Analysis using SQL

## 📌 Project Overview

This project focuses on analyzing retail sales data using SQL.  
The goal of this project is to perform:

- Data Cleaning
- Data Exploration
- Business Data Analysis
- Customer Insights
- Sales Trend Analysis

The project demonstrates practical SQL skills including:

- Aggregate Functions
- Window Functions
- Common Table Expressions (CTEs)
- Grouping & Filtering
- Ranking Functions
- Date & Time Functions

---

# 📂 Dataset Information

The dataset contains retail transaction records with details such as:

- Transaction ID
- Sale Date & Time
- Customer ID
- Gender
- Age
- Product Category
- Quantity
- Price Per Unit
- Cost of Goods Sold (COGS)
- Total Sale

📎 Dataset file is attached in this repository.

---

# 🛠️ Technologies Used

- SQL
- PostgreSQL

---

# 🗂️ Database & Table Creation

## Create Database

```sql
CREATE DATABASE sql_project1;
```

---

## Create Table

```sql
CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantiy INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

---

# 🧹 Data Cleaning

## Check Null Values

```sql
SELECT * 
FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR category IS NULL
   OR gender IS NULL
   OR quantiy IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

---

## Delete Null Values

```sql
DELETE FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR category IS NULL
   OR gender IS NULL
   OR quantiy IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

---

# 🔍 Data Exploration

## Total Sales

```sql
SELECT COUNT(*) AS total_sales 
FROM retail_sales;
```

---

## Total Customers

```sql
SELECT COUNT(DISTINCT customer_id) AS total_customers 
FROM retail_sales;
```

---

## Unique Categories

```sql
SELECT DISTINCT category 
FROM retail_sales;
```

---

# 📊 Data Analysis Queries

---

## Q1. Sales on Specific Date

```sql
SELECT * 
FROM retail_sales 
WHERE sale_date = '2022-11-05';
```

---

## Q2. Clothing Transactions with Quantity More Than 4

```sql
SELECT * 
FROM retail_sales
WHERE category = 'Clothing'
AND TO_CHAR(sale_date ,'YYYY-MM') = '2022-11'
AND quantiy >= 4;
```

---

## Q3. Total Sales by Category

```sql
SELECT 
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```

---

## Q4. Average Age of Beauty Customers

```sql
SELECT 
    ROUND(AVG(age),2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
```

---

## Q5. Transactions Greater Than 1000

```sql
SELECT * 
FROM retail_sales
WHERE total_sale > 1000;
```

---

## Q6. Transactions by Gender in Each Category

```sql
SELECT 
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
```

---

## Q7. Best Selling Month in Each Year

```sql
SELECT 
    year,
    month,
    avg_sale
FROM
(
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER(
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sales
    GROUP BY 1,2
) AS t1
WHERE rank = 1;
```

### 🔥 Concepts Used

- Window Functions
- RANK()
- PARTITION BY
- Aggregate Functions

---

## Q8. Top 5 Customers by Total Sales

```sql
SELECT
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```

---

## Q9. Unique Customers in Each Category

```sql
SELECT
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
```

---

## Q10. Orders by Shift (Morning / Afternoon / Evening)

```sql
WITH hourly_sale AS
(
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)

SELECT
    shift,
    COUNT(*) AS total_orders
FROM hourly_sale
GROUP BY shift;
```

---

# 📈 Key Insights & Findings

✔️ Identified top-performing sales months for each year.

✔️ Analyzed customer purchasing behavior based on category and gender.

✔️ Found high-value transactions above specific thresholds.

✔️ Discovered top customers contributing maximum revenue.

✔️ Analyzed order distribution across different daily shifts.

✔️ Performed complete data cleaning before analysis.

---

# 🚀 Skills Demonstrated

- SQL Query Writing
- Data Cleaning
- Data Analysis
- Window Functions
- Aggregate Functions
- CTEs
- Business Analytics
- Reporting

---

# 📁 Repository Structure

```text
Retail-Sales-Analysis/
│
├── README.md
├── retail_sales.sql
├── SQL - Retail Sales Analysis_utf.csv
└── screenshots/
```

---

# 👨‍💻 Author

## Saumya Gupta

B.Tech – Blockchain & Cyber Security  
Passionate about Data Analytics, SQL, Python, and Machine Learning.

---

# ⭐ Project Purpose

This project was created to strengthen SQL analytical skills and demonstrate real-world business data analysis using PostgreSQL.

---
````
