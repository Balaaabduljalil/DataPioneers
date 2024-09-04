# Exploratory Data Analysis of Posey Data Tables by DataPioneers Team (Group 3). 
# Table Of Contents. 
- Overview
- Aim of the Analysis
- Data
- Tools Used
- Notable Business Questions
- Insights
- Recommendation 

# Overview: 

Paper goods are the primary focus of the American business Parch & Posey. It employs fifty sales reps in all, who work in four US regions. Standard paper, glossy paper, and poster paper are the three types of paper that the company sells. Finding significant trends that can help with client retention, product promotion, sales growth, and well-informed company decisions is the goal of this analysis.

# Aim Of The Analysis: 

The purpose of this analysis is to gain valuable insights from the Company’s data and improve its sales performance.

# Data: 

The data underwent a comprehensive cleaning process prior to analysis. Every blank and duplication was removed. PostgreSQL was used for exploratory data analysis with the goal of minimizing revenue loss and optimizing revenue and sales. The CSV formatted results of the SQL queries were extracted, redirected, and entered into the visualization tool.

These four tables are found in the database of the Parch and Posey data company.
- Accounts
- Regions
- Orders
- Sales_reps
- Web_events
# Tool Used: 
PostgreSQL was used to generate queries that aid analytical and explorative analysis of the database.

# Notable Business Questions: 

What is the total, average quantity of product ordered, the total value and average?
``` SQL
SELECT 
	SUM(total) total_qty_ordered,
	ROUND(AVG(total), 2) average_qty_ordered,
	Sum(total_amt_usd) total_order_value_usd,
    	ROUND(AVG(total_amt_usd), 2) average_order_value_usd
FROM 
    orders; 
```

What is the total sales by product type?
```` SQL
SELECT 
    SUM(standard_amt_usd) standard_sales,
    SUM(gloss_amt_usd) gloss_sales,
    SUM(poster_amt_usd) poster_sales
FROM 
    orders;
````

What is the average sales by product type?
```` SQL
SELECT 
    ROUND(AVG(standard_amt_usd), 2) standard_sales,
    ROUND(AVG(gloss_amt_usd), 2) gloss_sales,
    ROUND(AVG(poster_amt_usd), 2) poster_sales
FROM 
    orders;
````

What is the total and average order value and quantity by year?
````SQL
SELECT 
    EXTRACT(year FROM occurred_at) as Year,
    SUM(total_amt_usd) total_order_value_usd,
    ROUND(AVG(total_amt_usd), 2) avg_order_value_usd,
    SUM(total) total_qty,
    ROUND(AVG(total), 2) avg_qty
FROM 
    orders
GROUP BY year
ORDER BY total_order_value_usd DESC;
````

What is the total and average order value and quantity by month?
````SQL
SELECT 
    EXTRACT(month FROM occurred_at) as month,
    SUM(total_amt_usd) total_order_value_usd,
    ROUND(AVG(total_amt_usd), 2) avg_order_value_usd,
    SUM(total) total_qty,
    ROUND(AVG(total), 2) avg_qty
FROM 
    orders
GROUP BY month
ORDER BY total_order_value_usd DESC;
````

What is the total and average order value and quantity by quarter?
````SQL
SELECT 
    EXTRACT(quarter FROM occurred_at) as quarter,
    SUM(total_amt_usd) total_order_value_usd,
    ROUND(AVG(total_amt_usd), 2) avg_order_value_usd,
    SUM(total) total_qty,
    ROUND(AVG(total), 2) avg_qty
FROM 
    orders
GROUP BY quarter
ORDER BY total_order_value_usd DESC;
````

When was the highest sales recorded?
```` SQL
SELECT
    DATE(occurred_at) AS sale_date, 
    SUM(total_amt_usd) AS total_sales 
FROM orders
GROUP BY sale_date
ORDER BY total_sales DESC
LIMIT 1;
````

When was the lowest sales recorded?
```` SQL
SELECT 
    DATE(occurred_at) sale_date, 
    SUM(total_amt_usd) total_sales 
FROM orders
GROUP BY sale_date
ORDER BY total_sales ASC
LIMIT 1;
````

TOP 5 Sales rep by total sales value and quantity sold?
```` SQL
SELECT 
    s.name sales_rep_name, 
    SUM(o.total_amt_usd) total_sales,
    SUM(o.total) total_qty
FROM orders o
LEFT JOIN accounts a
    ON o.account_id = a.id
LEFT JOIN sales_reps s
    ON a.sales_rep_id = s.id
GROUP BY sales_rep_name
ORDER BY total_sales DESC
LIMIT 5;
````

Account Distribution by Region
````SQL
SELECT 
    r.name AS region_name, 
    COUNT(a.id) AS number_of_accounts 
FROM 
    accounts a
LEFT JOIN sales_reps s
    ON a.sales_rep_id = s.id
LEFT JOIN region r
    ON s.region_id = r.id
GROUP BY 
    region_name
ORDER BY 
    number_of_accounts DESC;
````

Sales and quantity by Region
````SQL
SELECT 
    r.name region_name,
    COUNT(o.id) total_orders,
    SUM(o.total_amt_usd) total_sales_usd,
    ROUND(AVG(o.total_amt_usd), 2) avg_sales_usd,
    SUM(o.total) total_qty,
    ROUND(AVG(o.total), 2) avg_qty
FROM 
    orders o
LEFT JOIN accounts a
    ON o.account_id = a.id
LEFT JOIN sales_reps s
    ON a.sales_rep_id = s.id
LEFT JOIN region r
    ON s.region_id = r.id
GROUP BY region_name
ORDER BY total_sales_usd DESC;
````

4. What revenue is generated per company?
``` SQL
SELECT 
    a.name, 
    SUM(o.total_amt_usd) total_Sales
FROM orders AS o
JOIN accounts AS a 
   ON o.account_id = a.id
GROUP BY a.name
ORDER BY total_Sales DESC;
```


# Insights: 
Check out the presentation slides for the exploratory data analysis and recommendations. Thank




