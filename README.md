# 🚗 Veloza Motors SQL Project - Car Sales Analysis

![SQL](https://img.shields.io/badge/Tool-MySQL-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Data Source](https://img.shields.io/badge/Data-Car%20Sales%20%7C%20Customers%20%7C%20Dealers-lightgrey.svg)

> A structured SQL-based analysis project for **Veloza Motors**, uncovering key insights from car sales data. This report explores customer demographics, pricing patterns, dealer performance, and regional sales trends using SQL queries and database operations.

---

## 📌 Project Highlights

- 📊 **SQL data exploration** for sales, pricing, and demographic insights
- 🧼 **Data cleaning** techniques to ensure query reliability and accuracy
- 📈 **Revenue & pricing trend analysis** by model, body style, and region
- 🧍 **Customer demographic profiling** including income and gender distribution
- 🧑‍💼 **Dealer performance evaluation** based on total sales and revenue
- 🗺️ **Regional comparison** of car sales and brand diversity

---

## 🧪 Technologies Used

| Tool          | Purpose                               |
|---------------|---------------------------------------|
| MySQL 🐬       | Database engine for querying data     |
| SQL 🧮         | Writing queries for data analysis     |
| CSV 📂         | Source format for importing data      |
| Data Cleaning 🧹 | Ensuring valid, complete records     |

---

## 📂 Dataset Description

| Column Name     | Description                         |
|-----------------|-------------------------------------|
| Car_ID          | Unique identifier for each car sale |
| Purchase_Date   | Date of purchase                    |
| Customer_Name   | Name of the customer                |
| Gender          | Gender of the customer              |
| Annual_Income   | Annual income of the customer       |
| Dealer_Name     | Name of the dealer selling the car  |
| Company         | Car manufacturing brand             |
| Model           | Specific car model                  |
| Car_Engine      | Engine type of the car              |
| Transmission    | Type of transmission (Auto/Manual)  |
| Color           | Color of the car                    |
| Price ($)       | Sale price of the car               |
| Dealer_Number   | Unique identifier for the dealer    |
| Body_Style      | Car category (SUV, Passenger, etc.) |
| Phone           | Dealer's contact number             |
| Dealer_Region   | Region where the dealer is located  |

---

## 🎯 Project Objectives

- Analyze **customer demographics**: income, gender, buying behavior
- Identify **top-selling models, brands, and pricing trends**
- Evaluate **dealer-wise sales performance and revenue**
- Compare **regional sales output** and brand distribution

---

## 🛠️ SQL Implementation

### 1. 🔧 Database & Table Creation

```sql
CREATE DATABASE car_sales_project;
USE car_sales_project;

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

SELECT * FROM Car_sales;
```

### 2. 🧹 Data Cleaning
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

### 3. 🔍 Data Exploration Queries

3.1 Total Number of Records

```sql
SELECT COUNT(*) AS Total_Cars FROM Car_sales;
```

3.2 Unique Customers

```sql
SELECT COUNT(DISTINCT Customer_Name) AS Unique_Customers FROM Car_sales;
```

3.3 Unique Dealers, Companies, Models, Colors, Body Styles, and Regions

```sql
SELECT DISTINCT Dealer_Name FROM Car_sales;
SELECT DISTINCT Company FROM Car_sales;
SELECT DISTINCT Model FROM Car_sales;
SELECT DISTINCT Color FROM Car_sales;
SELECT DISTINCT Body_Style FROM Car_sales;
SELECT DISTINCT Dealer_Region FROM Car_sales;
```

---

## 📊 Analytical Insights
### 🧍 Customer Demographics
 * Unique customer count:
```sql
SELECT COUNT(DISTINCT Customer_Name) FROM Car_sales;
```
 *Gender distribution:
```sql
SELECT Gender, COUNT(*) FROM Car_sales GROUP BY Gender;
```
 * Average income:
```sql
SELECT AVG(Annual_Income) FROM Car_sales;
```
 * High-income customers:
```sql
SELECT COUNT(*) FROM Car_sales WHERE Annual_Income > 100000;
```
 * Highest income customer:
```sql
SELECT Customer_Name, Annual_Income 
FROM Car_sales 
ORDER BY Annual_Income DESC 
LIMIT 1;
```
 * Purchases per customer:
```sql
SELECT Customer_Name, COUNT(*) AS total_purchases 
FROM Car_sales 
GROUP BY Customer_Name 
ORDER BY total_purchases DESC;
```
 * Multiple purchases from same dealer:
```sql
SELECT Customer_Name, Dealer_Name, COUNT(*) AS cars_bought 
FROM Car_sales 
GROUP BY Customer_Name, Dealer_Name 
HAVING COUNT(*) > 1;
```

---

## 🚘 Car Sales & Pricing Trends
 * Total revenue:
```sql
SELECT SUM(Price) AS total_revenue FROM Car_sales;
```
 * Average car price:
```sql
SELECT AVG(Price) AS avg_price FROM Car_sales;
```
 * Max & Min prices:
```sql
SELECT MAX(Price) AS max_price, MIN(Price) AS min_price FROM Car_sales;
```
 * Sales by body style:
```sql
SELECT Body_Style, COUNT(*) FROM Car_sales GROUP BY Body_Style;
```
 * Top car model:
```sql
SELECT Model, COUNT(*) AS sales_count 
FROM Car_sales 
GROUP BY Model 
ORDER BY sales_count DESC 
LIMIT 1;
```
 * Most popular colors:
```sql
SELECT Color, COUNT(*) FROM Car_sales 
GROUP BY Color 
ORDER BY COUNT(*) DESC 
LIMIT 3;
```
 * Transmission type analysis:
```sql
SELECT Transmission, COUNT(*) FROM Car_sales GROUP BY Transmission;
```

---

## 🧑‍💼 Dealer & Regional Performance
 * Unique dealer count:
```sql
SELECT COUNT(DISTINCT Dealer_Name) FROM Car_sales;
```
 * Top dealer by sales:
```sql
SELECT Dealer_Name, COUNT(*) 
FROM Car_sales 
GROUP BY Dealer_Name 
ORDER BY COUNT(*) DESC 
LIMIT 1;
```
 * Top 30 dealers:
```sql
SELECT Dealer_Name, COUNT(*) 
FROM Car_sales 
GROUP BY Dealer_Name 
ORDER BY COUNT(*) DESC 
LIMIT 30;
```
 * Dealer-wise revenue:
```sql
SELECT Dealer_Name, SUM(Price) AS dealer_revenue 
FROM Car_sales 
GROUP BY Dealer_Name 
ORDER BY dealer_revenue DESC;
```
 * Regional sales comparison:
```sql
SELECT Dealer_Region, COUNT(*) 
FROM Car_sales 
GROUP BY Dealer_Region 
ORDER BY COUNT(*) DESC 
LIMIT 7;
```
 * Most sold brand per dealer:
```sql
SELECT Dealer_Name, Company, COUNT(*) AS total_sales 
FROM Car_sales 
GROUP BY Dealer_Name, Company 
ORDER BY Dealer_Name, total_sales DESC;
```
 * Brand diversity by region:
```sql
SELECT Dealer_Region, COUNT(DISTINCT Company) AS brand_count 
FROM Car_sales 
GROUP BY Dealer_Region;
```

---

## 📈 Key Business Insights
 * 💼 High-income customers are the top contributors to total revenue.
 * 🚙 SUVs and automatic transmission cars are preferred choices.
 * 🏆 Certain dealers outperform others in both volume and revenue.
 * 🎨 Car colors like white, black, and red dominate customer preferences.
 * 🌍 Regions with greater brand diversity show higher sales volume.

---

## 🧭 File Structure
```bash
veloza-motors-sql/
├── SQL/
│   └── car_sales_schema.sql          # Table creation scripts
│   └── car_sales_cleaning.sql        # Data cleaning queries
│   └── car_sales_analysis.sql        # Insights queries
├── Data/
│   └── car_sales.csv                 # Original dataset
└── README.md                         # Project documentation
```

---

## 🚀 Getting Started
 1. Clone the Repository

```bash
git clone https://github.com/your-username/veloza-motors-sql.git
cd veloza-motors-sql
```

 2. Launch MySQL and Run Scripts

  * Execute car_sales_schema.sql to create tables.
  * Import car_sales.csv into Car_sales table.
  * Run car_sales_cleaning.sql for data cleaning.
  * Explore with car_sales_analysis.sql.

---

## 📜 License
This project is licensed under the MIT License.
Use, share, and adapt freely with attribution.

---

## 🙌 Acknowledgments
 * 🚘 Thanks to Veloza Motors for the dataset concept.
 * 🛠️ To the SQL & MySQL community for supporting robust data tools.
 * 🌐 Special thanks to the open-source SQL learning ecosystem.

---

## 📫 Contact
For queries, suggestions, or collaboration: 📧 r.manisharathod6@gmail.com

---


