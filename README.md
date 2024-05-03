# Maven-Analytics-Restuarant-Order-Anlalysis

# Restaurant Order Analysis
# Overview
The Restaurant Analytics System is a data analytics project designed to provide insights and analysis for a restaurant business. It leverages data stored in MySQL databases and utilizes Jupyter Notebook as the primary analytical tool. The goal is to uncover valuable business insights, identify trends, and make data-driven decisions to enhance overall restaurant performance.

# Features
Sales and Revenue Analysis: Understand sales patterns, revenue generation, and identify top-selling items.
Customer Behavior Analysis: Analyze customer preferences, ordering habits, and identify popular menu categories.
Order Fulfillment Efficiency: Evaluate order processing times, peak hours, and identify areas for operational improvement.
Menu Optimization: Determine the most and least popular menu items to optimize the menu for better profitability.
Top Orders Analysis: Identify high-value orders and customer segments contributing significantly to revenue.
Performance Monitoring: Monitor the performance of the restaurant over time and identify areas for improvement.

# Requirements
Jupyter Notebook
MySQL database

# Installation
Clone the repository: https://github.com/rupalxxiii/Maven-Analytics-Restuarant-Order-Anlalysis 

# Install the required dependencies.
Set up the MySQL database using the provided SQL script:
Run the SQL script create_restaurant_db.sql to create the database and necessary tables.
Optionally, import sample data if available.

# Usage
Open Jupyter Notebook: jupyter notebook
Open the provided notebooks in the notebooks directory for data analysis and visualization.

# Data cleaning / preparation
    In the initial data preparation phase, we performed the following tasks:

1 Data loading and inspection.
2 Handling missing values.
3 Data cleaning and formatting.
4 Exploratory Data Analysis
5 EDA involved exploring the sales data to answer key questions, such as:
-----------------------------------------------------------------------------------------------------
Find the number of items on the menu.
What are the least and most expensive item on the menu ?
How many italian dishes are on the menu ?
What are the least and most expensive italian dishes on the menu ?
How many dishes are in each category ?
What is the average dish price within each category ?
What is the date range of the table ?
----------------------------------------------------------------------------------------------------
How many orders where made within this date range ?
How many items where ordered within this date range ?
Which orders had the most number of items ?
How many orders had more than 12 items ?
Combine the menu_items table and order_details table into a single table
----------------------------------------------------------------------------------------------------------
What were the least and most ordered items ? What categories where they in ?
What were the top 5 orders that spent the most money ?
View the details of the highest spent order. What insights can you gather from them ?
View the details of top 5 highest spent orders. What insights can you gather from them ?
---------------------------------------------------------------------------------------------------------
# Data analysis

1 View the menu_items table.
SELECT *
FROM menu_items;
-------------------------------------------------------------------------------------
2 Find the number of items on the menu
SELECT COUNT(*)
FROM menu_items;
-----------------------------------------------------------------------------------------
3 What are the least and most expensive item on the menu ?
SELECT *
FROM menu_items
ORDER BY price;
SELECT *
FROM menu_items
ORDER BY price DESC;
-------------------------------------------------------------------------------------------
3 How many italian dishes are on the menu ?
SELECT COUNT(*)
FROM menu_items
WHERE category = 'italian';
----------------------------------------------------------------------------------------------
4 What are the least and most expensive italian dishes on the menu ?
SELECT *
FROM menu_items
WHERE category = 'italian'
ORDER BY price;
SELECT *
FROM menu_items
WHERE category = 'italian'
ORDER BY price DESC;
How many dishes are in each category ?
SELECT category, COUNT(*)
FROM menu_items
GROUP BY category;
----------------------------------------------------------------------------------------------------
5 What is the average dish price within each category ?
SELECT category, AVG(price)
FROM menu_items
GROUP BY category;
---------------------------------------------------------------------------------------------------
6 View order_details table.
SELECT *
FROM order_details;
-----------------------------------------------------------------------------------------------
7 What is the date range of the table ?
SELECT MIN(order_date), max(order_date)
FROM order_details;
--------------------------------------------------------------------------------------------------
8 How many orders where made within this date range ?
SELECT COUNT(DISTINCT order_id)
FROM order_details;
-------------------------------------------------------------------------------------------------
9 How many items where ordered within this date range ?
SELECT COUNT(*)
FROM order_details;
--------------------------------------------------------------------------------------------------------
10 Which orders had the most number of items ?
SELECT order_id, COUNT(item_id) AS num_items
FROM order_details
GROUP BY order_id
ORDER BY num_items DESC;
------------------------------------------------------------------------------------------------------
11 How many orders had more than 12 items ?
SELECT COUNT(*)
FROM (SELECT order_id, COUNT(item_id) AS num_items
FROM order_details
GROUP BY order_id
HAVING num_items > 12) AS num_orders;
------------------------------------------------------------------------------------------------------
12 Combine the menu_items table and order_details table into a single table.
SELECT * FROM menu_items;
SELECT * FROM order_details;
SELECT * FROM order_details od LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id;
-------------------------------------------------------------------------------------------------------
13 What were the least and most ordered items ? What categories where they in ?
SELECT item_name, category, COUNT(order_details_id) AS num_purchases
FROM order_details od LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
GROUP BY item_name, category
ORDER BY num_purchases DESC;
------------------------------------------------------------------------------------------------------
14 What were the top 5 orders that spent the most money ?
SELECT order_id, SUM(price) AS total_spent
FROM order_details od LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
GROUP BY order_id
ORDER BY total_spent DESC
LIMIT 5 ;
--------------------------------------------------------------------------------------------------------
15 View the details of the highest spent order. What insights can you gather from them ?
SELECT *
FROM order_details od LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
WHERE order_id = 440 ;
-------------------------------------------------------------------------------------------------------------
16 View the details of top 5 highest spent orders. What insights can you gather from them ?
SELECT order_id, category, COUNT(item_id) AS num_items
FROM order_details od LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
WHERE order_id IN (440, 2075, 1957, 330, 2675 )
GROUP BY order_id, category;
-----------------------------------------------------------------------------------------------------------------

# Results / Findings

    The analysis results are summarized as follows:

1 The most and least expensive item in the Restaurant is Shrim scrampi (Italian) & Edamame (Asian).
2 The most and least ordered items are American Hamburger & Mexican Chicken Tacos.

# References
Maven Analytics.
