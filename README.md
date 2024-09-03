# Exploratory Data Analysis of Posey Data Tables by DataPioneers Team (Group 3). 
# Table Of Contents. 
- Overview
- Aim of the Analysis
- Data
- Tools Used
- Business Questions
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

# Business Questions: 
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
LIMIT 5; ```
