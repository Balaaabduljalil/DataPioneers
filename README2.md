# Exploratory Data Analysis of Posey Data Tables by DataPioneers Team (Group 3). 
### Table Of Contents. 
- Overview
- Aim of the Analysis
- Data
- Data cleaning
- Tools Used
- Notable Business Questions
- Insights
- Recommendation 

## Overview: 

Paper goods are the primary focus of the American business Parch & Posey. It employs fifty sales reps in all, who work in four US regions. Standard paper, glossy paper, and poster paper are the three types of paper that the company sells. Finding significant trends that can help with client retention, product promotion, sales growth, and well-informed company decisions is the goal of this analysis.

## Aim Of The Analysis: 

The purpose of this analysis is to gain valuable insights from the Company’s data and improve its sales performance.

## Data: 
The CSV files were loaded into the Posey database using Bash scripting. The database contains five tables: regions, orders, sales_reps, web_events, and accounts.
  
## Data Cleaning:
The data type for each column in the tables was modified to the appropriate type. Null values in the standard_qty, gloss_qty, and poster_qty columns of the orders table were replaced with 0. SQL query for data_cleaning can be found [here](Data_cleaning.md) No duplicate records were found in the database.

# Tool Used: 
PostgreSQL was used for explorative analysis of the database.

# Notable Business Questions: 

What is the total, average quantity of product ordered, the total value, and average?
``` SQL
SELECT 
	SUM(total) total_qty_ordered,
	ROUND(AVG(total), 2) average_qty_ordered,
	Sum(total_amt_usd) total_order_value_usd,
    	ROUND(AVG(total_amt_usd), 2) average_order_value_usd
FROM 
    orders; 
````
### Output:
total_qty_ordered | average_qty_ordered | total_order_value_usd | average_order_value_usd|
------------ | ------------ | ------------| ------------
3675765	| 533.34 | 23141511.83 |	3348.02


What is the total quantity by product type?
```` SQL
SELECT 
    SUM(standard_qty) total_standard_qty,
    SUM(gloss_qty) total_gloss_qty,
    SUM(poster_qty) total_poster_qty
FROM 
    orders;
````
### Output:
total_standard_qty | total_gloss_qty | total_poster_qty 
------------ | ------------ | ------------
1938346	| 1938346 | 723646


What is the average quantity by product type?
```` SQL
SELECT 
    ROUND(AVG(standard_qty), 2) avg_standard_qty,
    ROUND(AVG(gloss_qty), 2) avg_gloss_qty,
    ROUND(AVG(poster_qty), 2) avg_poster_qty
FROM 
    orders;
````
### Output:
avg_standard_qty | avg_gloss_qty | avg_poster_qty 
------------ | ------------ | ------------
280.43	| 146.67 | 104.69


What is the total sales by product type?
```` SQL
SELECT 
    SUM(standard_amt_usd) total_standard_sales,
    SUM(gloss_amt_usd) total_gloss_sales,
    SUM(poster_amt_usd) total_poster_sales
FROM 
    orders;
````
### Output:
total_standard_sales | total_gloss_sales | total_poster_sales 
------------ | ------------ | ------------
9672346.54	| 7593159.77 | 5876005.52


What is the average sales by product type?
```` SQL
SELECT 
    ROUND(AVG(standard_amt_usd), 2) avg_standard_sales,
    ROUND(AVG(gloss_amt_usd), 2) avg_gloss_sales,
    ROUND(AVG(poster_amt_usd), 2) avg_poster_sales
FROM 
    orders;
````
### Output:
avg_standard_sales | avg_gloss_sales | avg_poster_sales 
------------ | ------------ | ------------
1399.36	| 1098.55 | 850.12

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
### Output:
Year | total_order_value_usd | avg_order_value_usd | total_qty | avg_qty
------------ | ------------  | ------------ | ------------ | ------------
2016 | 12864917.92 | 3424.25 | 2041600 | 544.72
2015 | 5752004.94 | 3334.50 | 912972 | 530.18
2014 | 4069106.54 | 3115.70 | 650896 | 501.46
2013 | 377331.00 | 3811.42 | 58310 | 588.99
2017 | 78151.43 | 3126.06 | 11987 | 588.99



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
### Output:
month | total_order_value_usd | avg_order_value_usd | total_qty | avg_qty
------------ | ------------  | ------------ | ------------ | ------------
12 | 3129411.98 | 3548.09 | 486592 | 552.95
10 | 2427505.97 | 3596.31 | 386576 | 573.55
11 | 2390033.75 | 3352.08 | 377768 | 532.07
9 | 2017216.88| 3350.86 | 323082 | 537.57
7 | 1978731.15 | 3465.38 | 310849 | 546.31
8 | 1918107.22 | 3180.94 | 306756 | 508.72
6 | 1871118.52 | 3550.51 | 301487 | 572.08
3 | 1659987.88 | 3443.96 | 260453 | 542.61
4 | 1562037.74 | 3309.40 | 248033 | 527.73
5 | 1537082.23 | 2967.34 | 246816 | 478.33
1 | 1337661.87 | 2920.66 | 216438 | 474.64
2 | 1312616.64 | 3209.33 | 210915 | 519.50


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
### Output:
quarter | total_order_value_usd | avg_order_value_usd | total_qty | avg_qty
------------ | ------------  | ------------ | ------------ | ------------
4 | 7946951.70 | 3500.86 | 1250936 | 552.53
3 | 5914055.25 | 3329.99 | 940687 | 530.56
2 | 4970238.49 | 3276.36 | 796336 | 526.33
1 | 4310266.39 | 3195.16 | 687806 | 512.52



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
### Output:
sale_date | total_sales  
------------ | ------------ 
2016-12-26	| 297243.23 

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
### Output:
sale_date | total_sales  
------------ | ------------ 
2015-02-03	| 486.55

Top 5 Sales rep by total sales value and quantity sold?
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
### Output:
sales_rep_name | total_sales | total_qty 
------------ | ------------  | ------------ 
Earlie Schleusner | 70280814.08 | 11163520
Tia Amato | 64684198.40 | 9768832 
Vernita Plump | 59789627.52 | 9629888
Georgianna Chisholm | 56719623.68 | 8588672
Arica Stoltzfus | 51862613.76 | 7814592 


Top 5 Customers
```` SQL
SELECT 
    a.name account_name, 
    SUM(o.total_amt_usd) total_sales, 
	SUM(o.total) total_qty
FROM orders o
LEFT JOIN accounts a
	ON o.account_id = a.id
GROUP BY account_name
ORDER BY total_sales DESC
LIMIT 5;
````
### Output:
account_name | total_sales | total_qty 
------------ | ------------  | ------------ 
EOG Resources | 3062986.40 | 451280
Mosaic | 2764948.72 | 393968 
IBM | 2614555.84 | 380048
General Dynamics | 2405558.32 | 349840
Republic Services | 2350889.12 | 326664 


Account Distribution by Region
````SQL
SELECT 
    r.name AS region_name, 
    COUNT(s.name) AS number_of_accounts 
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
### Output:
region_name | number_of_accounts  
------------ | ------------ 
Northeast	| 54272
West	| 51712
Southeast	| 49152
Midwest	| 24576



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
### Output:
region_name | total_orders  | total_sales_usd  | avg_sales_usd  | total_qty  | avg_qty  
------------ | ------------  | ------------ | ------------ | ------------ | ------------
Northeast	| 1206784 | 3965135544.32 | 3285.70	| 629953536	| 524.23
West	| 1036288	| 3306750464.00	| 3190.96	| 529922560	| 512.38
Southeast	| 836608	| 3033662955.52	| 3626.15	| 474896384	| 569.74
Midwest	| 459264	| 1542905093.12	| 3359.52	| 247219200	| 538.29



Channels on Sales
````SQL
SELECT 
    w.channel, 
    SUM(o.total_amt_usd) total_sales,
    SUM(o.total) total_qty
FROM web_events w
LEFT JOIN orders o
     ON w.account_id = o.account_id
GROUP BY w.channel
ORDER BY total_sales DESC;
````
### Output:
channel | total_sales | total_qty 
------------ | ------------ | ------------
direct	| 5117598218.08 | 819264080
facebook	| 824245255.84 | 133458040
organic	| 816402614.24 | 133041680
adwords	| 782214845.12 | 127131016
twitter	| 405333525.52 | 66116208
banner	| 384627232.40 | 63330392

# Insights: 
Check out the presentation slides for the exploratory data analysis and recommendations. Thank




