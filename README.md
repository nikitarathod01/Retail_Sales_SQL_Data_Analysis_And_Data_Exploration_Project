# Retail_Sales_SQL_Data_Analysis_And_Data_Exploration_Project
Project Title: Retail Sales Data Analysis and Data Exploration
Level: Beginner
Database: Retail_sale_database

This project aims to showcase the SQL skills and techniques commonly employed by data analysts to explore, clean, and analyze retail sales data. It involves establishing a retail sales database, conducting exploratory data analysis (EDA), and addressing specific business questions through SQL queries. This project is particularly well-suited for individuals embarking on their data analysis journey who wish to build a strong foundation in SQL.

# Objectives
Set up a retail sales database: Create and populate a retail sales database with the provided sales data.
Data Cleaning: Identify and remove any records with missing or null values.
Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
Business Analysis: Use SQL to answer specific business questions and derive insights from the sales data.
# Project Structure
1. Database Setup
2. Install my-project with npm

```bash
  npm install my-project
  cd my-project
  
```
## Database Creation: The project starts by creating a database named p1_retail_db.
###Table Creation: A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, ###quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.
```
CREATE DATABASE p1_retail_db;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLO0AT
);
```



## 2. Data Exploration & Cleaning
## Record Count: Determine the total number of records in the dataset.
## Customer Count: Find out how many unique customers are in the dataset.
## Category Count: Identify all unique product categories in the dataset.

### Null Value Check: Check for any null values in the dataset and delete records with missing data.
```
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL, OR price_per_unit IS NULL, OR cogs IS NULL;
```
```
DELETE FROM retail_sales
WHERE 
    SELECT * FROM retail_sales
WHERE 
    transactions_id IS NULL
    OR
    sale_date IS NULL
    OR
    sale_time IS NULL
    OR
    customer_id IS NULL
    OR
    gender IS NULL
    OR
   age IS NULL
    OR
    category IS NULL
    OR
    quantiy IS NULL
    OR
    price_per_unit IS NULL
    OR
    cogs IS NULL
    OR
    total_sale IS NULL;

```

## 3. Data Analysis & Findings
###The following SQL queries were developed to answer specific business questions:


## 1. Write a SQL query to retrieve all columns for sales made on '2022-11-05:
```
SELECT *
FROM retail_sales                                   
WHERE sale_date = '2022-11-05'; 

```
## 2. Write a SQL query to retrieve all transactions where the category is 'Clothing,' and the quantity sold is more than 4 in the month of Nov-2022:
```
SELECT 
    category,
    SUM(quantity)
FROM retail_sales
WHERE category = 'Clothing'
    AND DAT
```
## 3. Write a SQL query to calculate the total sales (total_sale) for each category.:
```
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1;
```
## 4. Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.:
```
SELECT 
      AVG(age) as average_age
FROM  retail_sales 
WHERE category = 'Beauty';
```
## 5. Write a SQL query to find all transactions where the total_sale is greater than 1000.:
```
SELECT *
 FROM retail_sales
 WHERE total_sale > 1000;
```
## 6. Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.:
```
SELECT 
        category
        gender 
       COUNT(*) as total_trans
       FROM 
        retail_sales 
       GROUP BY 
        category 
        gender
       ORDER by 1;
```

## 7. Write a SQL query to calculate the average sale for each month. Find out best selling month in each year:
```  
SELECT * FROM
( SELECT 
   YEAR(sale_date) as year,
   MONTH(sale_date) as month,
   AVG(total_sale) as average_sale,
   RANK() OVER(PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC) AS sale_rank
FROM retail_sales
GROUP BY 1,2) as t1
WHERE sale_rank = 1;
```

## 8. Write a SQL query to find the top 5 customers based on the highest total sales **:
```
SELECT 
     customer_id,
     SUM(total_sale) AS total_sales
FROM 
     retail_sales
GROUP BY 
     customer_id
ORDER BY 2 DESC LIMIT 5;
```

## 9. Write a SQL query to find the number of unique customers who purchased items from each category.:
```
SELECT 
      category,
      COUNT(DISTINCT(customer_id)) as count_of_unique_customers
FROM retail_sales
GROUP BY category;
```

## 10. Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17):
```
WITH hourly_sale AS
(SELECT *,
      CASE 
         WHEN HOUR(sale_time) < 12 THEN 'Morning'
         WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
         ELSE 'Evening'
      END AS shift
      FROM retail_sales)
SELECT
     shift, 
     COUNT(*) as total_orders
FROM 
     hourly_sale
GROUP BY 
     shift;

```
# Findings
## Customer Demographics: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
## High-Value Transactions: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
## Sales Trends: Monthly analysis shows variations in sales, helping identify peak seasons.
## Customer Insights: The analysis identifies the top-spending customers and the most popular product categories.

# Reports
## Sales Summary: A detailed report summarizing total sales, customer demographics, and category performance.
## Trend Analysis: Insights into sales trends across different months and shifts.
## Customer Insights: Reports on top customers and unique customer counts per category.

# Conclusion
 ##This project provides a thorough introduction to SQL for data analysts, encompassing database setup, data cleaning, exploratory data analysis, and business-oriented SQL queries. The insights gained from this ##project can inform business decisions by revealing sales patterns, customer behavior, and product performance.
