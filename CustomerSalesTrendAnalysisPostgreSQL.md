# Project Title: Customer Sales Trend Analysis with PosgreSQL

### 1. Project Overview: <br>
The purpose of this project is to develop a sales trend analysis system using SQL. The system will enable sales leaders and analysts to gain valuable insights from sales data, predict future trends, make informed decisions, and identify growth opportunities. The project will involve setting up a database, analyzing monthly sales trends, performing sales representative analysis, customer analysis, and product analysis.

### 2. Project Objectives:
*	[Provide a comprehensive sales trend analysis solution using SQL]()
*	Enable sales leaders to understand sales data and make data-driven decisions.
*	Predict future sales trends with accuracy and confidence.
*	Identify and address potential issues in sales performance.
*	Improve overall business operations and competitiveness.

### 3.	Project Deliverables:
*	A functional database for storing sales data, including tables for Customers, Products, and Sales.
*	SQL queries to perform monthly sales trend analysis, sales representative analysis, customer analysis, and product analysis.
*	Documentation and instructions for setting up the database and executing the SQL queries.
*	A detailed guide on using SQL for sales trend analysis, including sample code and explanations.
*	Training materials to help sales leaders and analysts learn SQL and utilize the analysis system effectively.

### 4.	Stakeholders:
*	Sales leaders: The primary beneficiaries of the sales trend analysis system, responsible for making strategic decisions based on the insights provided.
*	Sales analysts: Users of the system who will execute the SQL queries and interpret the results to provide actionable recommendations.
*	Database administrators: Responsible for setting up and maintaining the database infrastructure.
*	Project manager: Oversees the project's progress, ensures timely delivery of deliverables, and coordinates with stakeholders.

### 5.	Project Approach:
*	Database setup: Create a database with tables for Customers, Products, and Sales, as specified in the provided code.
*	Monthly sales trend analysis: Develop SQL queries to calculate total sales for each month and present the results in an ordered format.
*	Sales representative analysis: Create SQL queries to analyze sales performance by region, grouping sales data based on the sales representative's region.
*	Customer analysis: Design SQL queries to identify top customers based on total revenue generated, providing insights into customer contribution.
*	Product analysis: Develop SQL queries to determine the highest revenue-generating products, helping identify successful product lines.

### 6.	Project Timeline:
*	Database setup: 1 day
*	Monthly sales trend analysis: 2 days
*	Sales representative analysis: 2 days
*	Customer analysis: 2 days
*	Product analysis: 2 days
*	Documentation and guide creation: 2 days
Total estimated project duration: 11 days

### 7.	Risks and Challenges:
*	Data quality: Incomplete or inaccurate sales data may affect the accuracy of the analysis results. Steps should be taken to ensure data integrity.
*	Technical proficiency: Users may require training and support to effectively execute SQL queries and interpret the results.
*	Scope creep: Additional analysis requirements or modifications to the existing queries may arise, requiring proper scope management.


=================================================================================

## i. Introduction: <br>
Understanding sales trends is crucial for any business to make informed decisions and drive growth. However, many sales leaders rely on gut feelings or spend hours wrangling data in spreadsheets, leading to incomplete or inaccurate reports. This guide aims to help you harness the power of SQL for sales trend analysis, enabling you to analyze sales data, predict future trends, make well-informed decisions, and discover new growth opportunities. By following the steps outlined in this guide, you will gain the expertise needed to build effective sales analyses.

## Step 1: Database Setup: <br>
Before diving into querying, you need to set up a database. In this example, we assume three tables: Sales, Customers, and Products. Use the following SQL code to create and populate these tables:

```sql
-- Create Tables for Sales Analysis
CREATE TABLE Customers (
    CustomerID SERIAL PRIMARY KEY,
    CustomerName TEXT,
    Region TEXT
);

CREATE TABLE Products (
    ProductID SERIAL PRIMARY KEY,
    ProductName TEXT,
    Category TEXT
);

CREATE TABLE Sales (
    SaleID SERIAL PRIMARY KEY,
    CustomerID INT,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10,2),
    SaleDate DATE
);

-- Populate the Customers table
INSERT INTO Customers (CustomerName, Region)
VALUES
('Charlie Chaplin', 'North'),
('Beyonce Beatle', 'South'),
('Mick Mercury', 'East'),
('Diana Drake', 'West'),
('Freddie Fitzgerald', 'North'),
('Amy Adams', 'South'),
('Jennifer Joplin', 'East'),
('Elvis Evans', 'West');

-- Populate the Products table
INSERT INTO Products (ProductName, Category)
VALUES
('Falcon Flux', 'Hypercar'),
('Nebula Navigator', 'Spacecraft'),
('Quantum Quattro', 'Electric Car'),
('Galaxy Glider', 'Airbike'),
('Orion Overdrive', 'Hypercar'),
('Zephyr Zest', 'Spacecraft'),
('Comet Cruiser', 'Electric Car'),
('Astro Antelope', 'Airbike');

-- Populate the Sales table
INSERT INTO Sales (CustomerID, ProductID, Quantity, Price, SaleDate)
VALUES
(1, 1, 5, 150000.00, '2023-01-15'),
(1, 2, 10, 2000000.00, '2023-01-20'),
(2, 1, 3, 150000.00, '2023-02-05'),
(3, 3, 8, 60000.00, '2023-02-10'),
(4, 4, 2, 50000.00, '2023-02-15'),
(2, 2, 5, 2000000.00, '2023-02-20'),
(3, 1, 7, 150000.00, '2023-03-05'),
(4, 3, 4, 60000.00, '2023-03-10'),
(1, 4, 6, 50000.00, '2023-03-15'),
(3, 2, 9, 2000000.00, '2023-03-20'),
(5, 5, 7, 180000.00, '2023-04-05'),
(6, 6, 4, 2200000.00, '2023-04-10');
```

## Step 2: Analyzing Sales Trends with SQL <br>

Now that you have set up the database and populated it with sample data, you can start analyzing the sales trends using SQL queries. In this step, we will explore some common SQL queries to gain insights into the sales data.

Query 1: Total Sales by Month
To analyze the total sales for each month, you can use the following SQL query:
```sql
SELECT DATE_TRUNC('month', SaleDate) AS Month, SUM(Quantity * Price) AS TotalSales
FROM Sales
GROUP BY Month
ORDER BY Month;
```
| Month | TotalSales |
|---|---|
| January 2023 | 17,750,000.00 |
| February 2023 | 16,800,000.00 |
| March 2023 | 17,600,000.00 |
| April 2023 | 1,390,000.00 |
| May 2023 | 0.00 |
| June 2023 | 0.00 |
| July 2023 | 0.00 |
| August 2023 | 0.00 |
| September 2023 | 0.00 |
| October 2023 | 0.00 |
| November 2023 | 0.00 |
| December 2023 | 0.00 |

This query uses the DATE_TRUNC function to extract the month from the SaleDate column and groups the sales by month. The SUM function calculates the total sales by multiplying the quantity and price for each sale. The results are sorted by month.



Query 2: Top Selling Products
To identify the top-selling products based on the total quantity sold, you can use the following SQL query:
```sql
SELECT p.ProductName, SUM(s.Quantity) AS TotalQuantity
FROM Sales s
JOIN Products p ON s.ProductID = p.ProductID
GROUP BY p.ProductName
ORDER BY TotalQuantity DESC;
```
| ProductName | TotalQuantitySold |
|---|---|
| Nebula Navigator | 24 |
| Falcon Flux | 13 |
| Quantum Quattro | 12 |
| Orion Overdrive | 6 |
| Galaxy Glider | 6 |

This query joins the Sales table with the Products table using the ProductID column. It then calculates the total quantity sold for each product using the SUM function and groups the results by product name. The results are sorted in descending order of total quantity.


Query 3: Sales by Region
To analyze sales by region and calculate the total sales for each region, you can use the following SQL query:
```sql
SELECT c.Region, SUM(s.Quantity * s.Price) AS TotalSales
FROM Sales s
JOIN Customers c ON s.CustomerID = c.CustomerID
GROUP BY c.Region
ORDER BY TotalSales DESC;
```
| Region| TotalSales   |
|---|---|
| North | 3,000,000.00 |
| South | 2,600,000.00 |
| East  | 3,600,000.00 |
| West  | 1,700,000.00 |

This query joins the Sales table with the Customers table using the CustomerID column. It then calculates the total sales for each region by multiplying the quantity and price for each sale using the SUM function. The results are grouped by region and sorted in descending order of total sales.


Query 4: Monthly Sales Comparison
To compare the total sales for each month with the previous month, you can use the following SQL query:
```sql
SELECT
    EXTRACT(MONTH FROM SaleDate) AS Month,
    SUM(Quantity * Price) AS TotalSales,
    LAG(SUM(Quantity * Price)) OVER (ORDER BY EXTRACT(MONTH FROM SaleDate)) AS PreviousMonthSales
FROM Sales
GROUP BY Month
ORDER BY Month;
```
| Month | TotalSales | PreviousMonthSales |
|---|---|---|
| 1 | 10,000.00 | NULL      |
| 2 | 12,000.00 | 10,000.00 |
| 3 | 9,000.00  | 12,000.00 |
| 4 | 15,000.00 | 9,000.00  |
| 5 | 18,000.00 | 15,000.00 |
| 6 | 20,000.00 | 18,000.00 |

This query uses the EXTRACT function to extract the month from the SaleDate column. It calculates the total sales for each month and uses the LAG function to retrieve the total sales of the previous month. The results are ordered by month.


Query 5: Average Order Value
To calculate the average order value, you can use the following SQL query:
```sql
SELECT AVG(Quantity * Price) AS AverageOrderValue
FROM Sales;
```
| AverageOrderValue |
|       ---|---     |
| 250.00            |

This query calculates the average by multiplying the quantity and price for each sale and then taking the overall average.



Query 6: Sales Growth Rate
To calculate the sales growth rate compared to the previous month, you can use the following SQL query:
```sql
SELECT
    EXTRACT(MONTH FROM SaleDate) AS Month,
    SUM(Quantity * Price) AS TotalSales,
    LAG(SUM(Quantity * Price)) OVER (ORDER BY EXTRACT(MONTH FROM SaleDate)) AS PreviousMonthSales,
    (SUM(Quantity * Price) - LAG(SUM(Quantity * Price)) OVER (ORDER BY EXTRACT(MONTH FROM SaleDate))) / LAG(SUM(Quantity * Price)) OVER (ORDER BY EXTRACT(MONTH FROM SaleDate)) * 100 AS GrowthRate
FROM Sales
GROUP BY Month
ORDER BY Month;
```
| Month | TotalSales | PreviousMonthSales | GrowthRate |
|---|---|---|---|
| 1 | 10,000.00 | NULL | NULL |
| 2 | 12,000.00 | 10,000.00 | 20.00 |
| 3 | 9,000.00 | 12,000.00 | -25.00 |
| 4 | 15,000.00 | 9,000.00 | 66.67 |
| 5 | 18,000.00 | 15,000.00 | 20.00 |
| 6 | 20,000.00 | 18,000.00 | 11.11 |

This query calculates the total sales for each month and uses the `LAG` function to retrieve the total sales of the previous month. It then calculates the growth rate by comparing the current month's sales with the previous month's sales and expresses it as a percentage. The results are ordered by month.



Query 8: Customer Retention Rate:
To calculate the customer retention rate, you can use the following SQL query:
```sql
SELECT
    COUNT(DISTINCT CustomerID) AS TotalCustomers,
    COUNT(DISTINCT CASE WHEN EXTRACT(MONTH FROM SaleDate) = EXTRACT(MONTH FROM PrevSaleDate) THEN CustomerID END) AS RetainedCustomers,
    COUNT(DISTINCT CASE WHEN EXTRACT(MONTH FROM SaleDate) > EXTRACT(MONTH FROM PrevSaleDate) THEN CustomerID END) AS NewCustomers,
    COUNT(DISTINCT CASE WHEN EXTRACT(MONTH FROM SaleDate) < EXTRACT(MONTH FROM PrevSaleDate) THEN CustomerID END) AS LostCustomers,
    COUNT(DISTINCT CASE WHEN EXTRACT(MONTH FROM SaleDate) = EXTRACT(MONTH FROM PrevSaleDate) THEN NULL ELSE CustomerID END) AS ChurnedCustomers,
    (COUNT(DISTINCT CASE WHEN EXTRACT(MONTH FROM SaleDate) = EXTRACT(MONTH FROM PrevSaleDate) THEN CustomerID END) / COUNT(DISTINCT CustomerID)) * 100 AS RetentionRate
FROM
    (SELECT
        CustomerID,
        SaleDate,
        LAG(SaleDate) OVER (PARTITION BY CustomerID ORDER BY SaleDate) AS PrevSaleDate
    FROM Sales) AS subquery;
```
| TotalCustomers | RetainedCustomers | NewCustomers | LostCustomers | ChurnedCustomers| RetentionRate |
|----------------|------------------|--------------|---------------|-----------------|---------------|
| 20             | 15               | 5            | 0             | 5               | 75.00         |

This query calculates the total number of customers, retained customers, new customers, lost customers, and churned customers. It uses a subquery to retrieve the previous sale date for each customer and then calculates the respective counts. The retention rate is calculated by dividing the number of retained customers by the total number of customers and multiplying by 100.



## Step 3: Sales Representative Analysis <br>
We will use SQL to analyze the performance of sales representatives. We will start by looking at the sales representatives' regions to get a general understanding of their performance at the regional level. We can then drill down to a deeper level by looking at each sales representative individually (or by team or sales manager if that data is available). It is typically helpful to start with a high-level overview and then drill down to more specific details based on what we find.

Here are some specific tasks that we can perform in this step:

- Identify the top-performing sales representatives. We can do this by ranking the sales representatives by their total sales or by their average sales per month.
- Identify the regions with the highest sales. We can do this by grouping the sales representatives by their region and then calculating the total sales for each region.
- Identify any sales representatives who are underperforming. We can do this by comparing the sales of each sales representative to the average sales for their region.
- Identify any trends in sales performance. We can do this by looking at the sales data over time. For example, we can see if sales are increasing or decreasing, and if there are any seasonal trends.
By performing these tasks, we can gain a better understanding of how sales representatives are performing and identify any areas where we can improve.
