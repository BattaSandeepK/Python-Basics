Project Overview
Project Title: Retail Sales Analysis
Level: Beginner
Database:retail_db

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in SQL.

Objectives
Set up a retail sales database: Create and populate a retail sales database with the provided sales data.
Data Cleaning: Identify and remove any records with missing or null values.
Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
Business Analysis: Use SQL to answer specific business questions and derive insights from the sales data.
Project Structure
1. Database Setup
Database Creation: The project starts by creating a database named p1_retail_db.
Table Creation: A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.
CREATE DATABASE p1_retail_db;

CREATE TABLE retail_sales
(
    Transactions_id INT PRIMARY KEY,
    Trans_Date DATE,	
    Customer_ID INT,	
    Gender VARCHAR(10),
    Age INT,
    Product_Category VARCHAR(35),
    Quantity INT,
    Price_per_unit FLOAT,	
    Total_Amount FLOAT
);
2. Data Exploration & Cleaning
Record Count: Determine the total number of records in the dataset.
Customer Count: Find out how many unique customers are in the dataset.
Category Count: Identify all unique product categories in the dataset.
Null Value Check: Check for any null values in the dataset and delete records with missing data.
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT Customer_ID) FROM retail_sales;
SELECT DISTINCT Product_Category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    Trans_Date IS NULL OR Customer_ID IS NULL OR 
    Gender IS NULL OR Age IS NULL OR  Product_Category IS NULL OR 
    Quantity IS NULL OR Price_per_unit IS NULL;

DELETE FROM retail_sales
WHERE 
    Trans_Date IS NULL OR Customer_ID IS NULL OR 
    Gender IS NULL OR Age IS NULL OR  Product_Category IS NULL OR 
    Quantity IS NULL OR Price_per_unit IS NULL;
3. Data Analysis & Findings
The following SQL queries were developed to answer specific business questions:

Write a SQL query to retrieve all columns for sales made on '2023-10-07:
SELECT *
FROM retail_sales
WHERE Trans_Date = '2023-10-07';
Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 5 in the month of Oct-2023:
SELECT 
  *
FROM retail_sales
WHERE 
    Product_Category = 'Clothing'
    AND 
    TO_CHAR(Trans_Date, 'YYYY-MM') = '2023-10'
    AND
    quantity >= 5
Write a SQL query to calculate the total sales (total_sale) for each category.:
SELECT 
    category,
    SUM(Total_Amount) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1
Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.:
SELECT
    ROUND(AVG(Age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'
Write a SQL query to find all transactions where the total_sale is greater than 1000.:
SELECT * FROM retail_sales
WHERE Total_Amount > 1000
Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.:
SELECT 
    Product_Category,
    Gender,
    COUNT(*) as total_trans
FROM retail_sales
GROUP 
    BY 
    Product_Category,
    Gender
ORDER BY 1
Write a SQL query to calculate the average sale for each month. Find out best selling month in each year:
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    EXTRACT(YEAR FROM Trans_Date) as year,
    EXTRACT(MONTH FROM Trans_Date) as month,
    AVG(Total_Amount) as avg_sale,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM Trans_Date) ORDER BY AVG(Total_Amount) DESC) as rank
FROM retail_sales
GROUP BY 1, 2
) as t1
WHERE rank = 1
**Write a SQL query to find the top 5 customers based on the highest total sales **:
SELECT 
    Customer_ID,
    SUM(Total_Amount) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5
Write a SQL query to find the number of unique customers who purchased items from each category.:
SELECT 
    Product_Category,    
    COUNT(DISTINCT Customer_ID) as cnt_unique_cs
FROM retail_sales
GROUP BY Product_Category

Findings
Customer Demographics: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
High-Value Transactions: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
Sales Trends: Monthly analysis shows variations in sales, helping identify peak seasons.
Customer Insights: The analysis identifies the top-spending customers and the most popular product categories.
Reports
Sales Summary: A detailed report summarizing total sales, customer demographics, and category performance.
Trend Analysis: Insights into sales trends across different months and shifts.
Customer Insights: Reports on top customers and unique customer counts per category.
Conclusion
This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

How to Use
Clone the Repository: Clone this project repository from GitHub.
Set Up the Database: Run the SQL scripts provided in the database_setup.sql file to create and populate the database.
Run the Queries: Use the SQL queries provided in the analysis_queries.sql file to perform your analysis.
Explore and Modify: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.
