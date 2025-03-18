Veloza Motors SQL Project - Car Sales Analysis

Project Overview

This project focuses on analyzing car sales data from Veloza Motors using SQL. The dataset contains information on customers, dealerships, car models, pricing, and sales trends. Through SQL queries, we aim to extract key insights related to **customer demographics, pricing patterns, dealer performance, and regional sales distribution.


Dataset Description

The dataset consists of the following columns:

| Column Name       | Description                         |
|-------------------|-------------------------------------|
| Car_ID            | Unique identifier for each car sale |
| Purchase_Date     | Date of purchase                    |
| Customer_Name     | Name of the customer                |
| Gender            | Gender of the customer              |
| Annual_Income     | Annual income of the customer       |
| Dealer_Name       | Name of the dealer selling the car  |
| Company           | Car manufacturing brand             |
| Model             | Specific car model                  |
| Car_Engine        | Engine type of the car              |
| Transmission      | Type of transmission (Auto/Manual)  |
| Color             | Color of the car                    |
| Price ($)         | Sale price of the car               |
| Dealer_Number     | Unique identifier for the dealer    |
| Body_Style        | Car category (SUV, Passenger, etc.) |
| Phone             | Dealer's contact number             |
| Dealer_Region     | Region where the dealer is located  |


Project Objectives

This project aims to answer key business questions such as:
- Customer Demographics: Understanding customer distribution, income levels, and purchasing behavior.
- Sales & Pricing Trends: Identifying revenue, pricing patterns, and popular car models.
- Dealer & Regional Insights: Evaluating dealership performance and regional sales trends.


SQL Implementation

1. Database & Table Creation
First, we created a database and table to store the data.

```sql
-- Creating the database
CREATE DATABASE car_sales_project;
USE car_sales_project;

-- Creating the table
CREATE TABLE Car_sales ( 
    Car_ID VARCHAR(50) PRIMARY KEY,
    Purchase_Date DATE,
    Customer_Name VARCHAR(50),
    Gender VARCHAR(10),
    Annual_Income FLOAT,
    Dealer_Name VARCHAR(50),
    Company VARCHAR(50),
    Model VARCHAR(50),
    Car_Engine VARCHAR(50),
    Transmission VARCHAR(50),
    Color VARCHAR(50),
    Price FLOAT,
    Dealer_Number VARCHAR(15),
    Body_Style VARCHAR(50),
    Phone VARCHAR(15),
    Dealer_Region VARCHAR(50)
);

-- Viewing the table data
SELECT * FROM Car_sales;
```

After creating the database and table in MySQL, we imported the CSV file.

2. Data Cleaning
Second, we executed the following data cleaning queries to remove any records containing null values in critical fields.

```sql
SET sql_safe_updates = 0;

DELETE FROM Car_sales
WHERE 
    Car_ID IS NULL OR
    Purchase_Date IS NULL OR
    Customer_Name IS NULL OR 
    Gender IS NULL OR
    Annual_Income IS NULL OR
    Dealer_Name IS NULL OR
    Company IS NULL OR
    Model IS NULL OR
    Car_Engine IS NULL OR
    Transmission IS NULL OR
    Color IS NULL OR
    Price IS NULL OR
    Dealer_Number IS NULL OR
    Body_Style IS NULL OR
    Phone IS NULL OR
    Dealer_Region IS NULL;
```
This step ensures data integrity by eliminating incomplete records that could affect the accuracy of the analysis.

3. Data Exploration
After completing the data cleaning process, we conducted an initial data exploration using SQL queries to gain insights into key aspects of the dataset. The following SQL commands were executed:  

 3.1 Total number of car sales records
  ```sql
   SELECT COUNT(*) AS Total_Cars FROM Car_sales;
  ```

 3.2 Unique number of customers  
  ```sql
   SELECT COUNT(DISTINCT Customer_Name) AS Unique_Customers FROM Car_sales;
  ```

 3.3 Unique number of dealers
  ```sql
   SELECT DISTINCT Dealer_Name FROM Car_sales;
  ```

 3.4 Unique number of car companies
  ```sql
   SELECT DISTINCT Company FROM Car_sales;
  ```

 3.5 Unique number of car models
  ```sql
   SELECT DISTINCT Model FROM Car_sales;
  ```

 3.6 Unique number of car colors
  ```sql
   SELECT DISTINCT Color FROM Car_sales;
  ```
 3.7 Unique number of car body styles
  ```sql
   SELECT DISTINCT Body_Style FROM Car_sales;
  ```

3.8 Unique number of dealer regions
 ```sql
  SELECT DISTINCT Dealer_Region FROM Car_sales;
 ```

This exploration provided an overview of the dataset's structure, including the number of distinct customers, dealers, car companies, models, colors, body styles, and dealer regions. These insights served as a foundation for further in-depth analysis.


SQL Queries & Insights

1. Customer & Demographics Analysis

1.1 How many unique customers are in the dataset?
```sql
SELECT COUNT(DISTINCT Customer_Name) AS unique_customers FROM Car_sales;
```

1.2 What is the distribution of customers by gender?
```sql
SELECT Gender, COUNT(*) AS customer_count FROM Car_sales GROUP BY Gender;
```

1.3 What is the average annual income of customers?
```sql
SELECT AVG(Annual_Income) AS avg_income FROM Car_sales;
```

1.4 How many customers have an annual income above $100,000?
```sql
SELECT COUNT(*) AS high_income_customers FROM Car_sales WHERE Annual_Income > 100000;
```

1.5 Which customer has the highest annual income?
```sql
SELECT Customer_Name, Annual_Income FROM Car_sales 
ORDER BY Annual_Income DESC LIMIT 1;
```

1.6 What is the total number of cars purchased per customer?  
```sql
SELECT Customer_Name, COUNT(*) AS total_purchases 
FROM Car_sales 
GROUP BY Customer_Name 
ORDER BY total_purchases DESC;
```

1.7 How many customers bought multiple cars from the same dealer?
```sql
SELECT Customer_Name, Dealer_Name, COUNT(*) AS cars_bought 
FROM Car_sales 
GROUP BY Customer_Name, Dealer_Name 
HAVING COUNT(*) > 1;
```


2. Car Sales & Pricing Analysis

2.1 What is the total revenue generated from car sales?
```sql
SELECT SUM(Price) AS total_revenue FROM Car_sales;
```

2.2 What is the average price of a car in the dataset?
```sql
SELECT AVG(Price) AS avg_price FROM Car_sales;
```

2.3 What is the highest and lowest car price in the dataset?
```sql
SELECT 
    MAX(Price) AS max_price, 
    MIN(Price) AS min_price 
FROM Car_sales;
```

2.4 How many SUVs vs. Passenger cars were sold?
```sql
SELECT Body_Style, COUNT(*) AS total_sales 
FROM Car_sales 
GROUP BY Body_Style;
```

2.5 Which car model has the highest sales count?
```sql
SELECT Model, COUNT(*) AS sales_count 
FROM Car_sales 
GROUP BY Model 
ORDER BY sales_count DESC 
LIMIT 1;
```

2.6 Which color of car is most frequently purchased?
```sql
SELECT Color, COUNT(*) AS color_count 
FROM Car_sales 
GROUP BY Color 
ORDER BY color_count DESC 
LIMIT 1;
```

2.7 What is the distribution of car sales by transmission type (Auto vs. Manual)?
```sql
SELECT Transmission, COUNT(*) AS total_sales 
FROM Car_sales 
GROUP BY Transmission;
```


3. Dealer & Regional Insights

3.1 How many unique dealers are present in the dataset?
```sql
SELECT COUNT(DISTINCT Dealer_Name) AS unique_dealers FROM Car_sales;
```

3.2 Which dealer has the highest number of car sales?
```sql
SELECT Dealer_Name, COUNT(*) AS total_sales 
FROM Car_sales 
GROUP BY Dealer_Name 
ORDER BY total_sales DESC 
LIMIT 1;
```

3.3 What is the total revenue generated per dealer?
```sql
SELECT Dealer_Name, SUM(Price) AS dealer_revenue 
FROM Car_sales 
GROUP BY Dealer_Name 
ORDER BY dealer_revenue DESC;
```

3.4 What are the top 5 dealer regions with the highest number of sales?
```sql
SELECT Dealer_Region, COUNT(*) AS total_sales 
FROM Car_sales 
GROUP BY Dealer_Region 
ORDER BY total_sales DESC 
LIMIT 5;
```

3.5 What is the most common car brand (Company) sold by each dealer?
```sql
SELECT Dealer_Name, Company, COUNT(*) AS total_sales 
FROM Car_sales 
GROUP BY Dealer_Name, Company 
ORDER BY Dealer_Name, total_sales DESC;
```

3.6 How many different brands are sold in each dealer region?
```sql
SELECT Dealer_Region, COUNT(DISTINCT Company) AS brand_count 
FROM Car_sales 
GROUP BY Dealer_Region;
```


Conclusion

This SQL project provided valuable insights into customer demographics, sales trends, and dealership performance for Veloza Motors. Some key findings include:
- High-income customers contribute significantly to sales.
- SUVs and automatic transmission cars are in high demand.
- Top-performing dealers and regions drive major sales.
- Certain car colors and models are consistently preferred.

These insights help in strategic planning, inventory management, and marketing decisions.


Technology & Tools Used
- Database Management System: MySQL.
- Query Language: SQL.
- Data Processing: Data cleaning and transformation techniques applied.
