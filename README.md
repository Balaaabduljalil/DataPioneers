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
- Sales_Reps
- Web_event
# Tool Used: 
PostgreSQL was used to generate queries that aid analytical and explorative analysis of the database.

# Notable Business Questions: 
1. Who are the top 5 customers with more than 30 orders, including their product preferences?

``` SQL

SELECT 
    Name,
    SUM(CASE WHEN poster_qty > 30 THEN 1 ELSE 0 END) AS Poster_Count,
    SUM(CASE WHEN gloss_qty > 30 THEN 1 ELSE 0 END) AS Gloss_Count,
    SUM(CASE WHEN standard_qty > 30 THEN 1 ELSE 0 END) AS Standard_Count
FROM orders AS o
JOIN accounts AS a 
ON o.account_id = a.id
GROUP BY 
    Name
ORDER BY 
    Poster_Count DESC, Gloss_Count DESC, Standard_Count DESC
LIMIT 5; 
```
2. What is the total sales made and their distribution across each documented year (2014-2017)?
``` SQL
SELECT
    DATE_PART('year', occurred_at) AS Year,
    SUM(total_amt_usd) AS Total_Sales
FROM
    orders
GROUP BY 
   Year
ORDER BY 
    Year;
```
3. What is the total monthly revenue per year from 2014-2017?

``` SQL
SELECT
    DATE_PART('Year', occurred_at) AS Year,
    DATE_PART('month', occurred_at) AS Month,
 SUM(total_amt_usd) AS Total_Sales
FROM orders
GROUP BY
    Year, Month
ORDER BY 
     Year;
```
4. What revenue is generated per company?
``` SQL
SELECT 
    a.Name, 
    SUM(o.total_amt_usd) AS Total_Sales
FROM 
    orders AS o
JOIN 
    accounts AS a 
ON 
    o.account_id = a.id
GROUP BY 
    a.Name
ORDER BY 
    Total_Sales DESC;
```
5. What is the performance of sales representatives who have both the highest number of orders and the highest revenue generated?
``` SQL
SELECT 
s.name As sales_reps, 
COUNT(o.total) as Total_Orders, 
	SUM(total_amt_usd) as Total_Revenue
FROM sales_reps as s
JOIN accounts as a
ON s.id = a.sales_rep_id
JOIN orders as o
ON a.id = o.account_id
GROUP BY
s.Name
ORDER BY 
Total_Revenue DESC
```
6. What region(s) that have generated the highest total revenue?
``` SQL
SELECT 
region.Name,   
        	sum(standard_amt_usd) as Total_Standard_Amt,
	sum(gloss_amt_usd) as Total_Gloss_Amt,
	sum(poster_amt_usd) as Poster_Amt
FROM sales_reps
JOIN region
ON sales_reps.region_id = region.id
JOIN accounts
ON accounts.sales_rep_id = sales_reps.id
JOIN orders
ON orders.account_id = accounts.id
GROUP BY 
    region.id, region.Name
ORDER BY
   region.id
```
# Insights: 




