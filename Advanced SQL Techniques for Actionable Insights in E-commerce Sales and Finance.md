# Advanced SQL Techniques for Actionable Insights in E-commerce Sales and Finance 

Structured Query Language (SQL) is a powerful tool for managing and manipulating data stored in databases. While basic SQL commands like SELECT, INSERT, UPDATE, and DELETE are suitable for many common use cases, advanced techniques can enable more complex queries and analyses. In this guide, we will explore some of the most popular advanced SQL techniques with a focus on e-commerce sales and finance data.

## 1. Window Functions 
Window functions are useful for identifying trends and patterns in e-commerce sales data. Let's consider an example of using a window function to calculate monthly sales growth rates:

```sql
SELECT month, total_sales,
       LAG(total_sales) OVER (ORDER BY month) AS previous_month_sales,
       (total_sales - LAG(total_sales) OVER (ORDER BY month)) / LAG(total_sales) OVER (ORDER BY month) * 100 AS growth_rate
FROM sales_table;
```

**Explanation:**
- The query retrieves the month and total sales from the 'sales_table'.
- The 'LAG()' function is used with the 'OVER' clause to fetch the total sales for the previous month. This allows us to compare the current month's sales with the previous month's sales.
- We calculate the growth rate by subtracting the previous month's sales from the current month's sales, dividing it by the previous month's sales, and multiplying by 100 to get a percentage.
This query helps identify the monthly growth rate of sales, allowing Spring GDS Hong Kong to track performance, identify trends, and make informed decisions on marketing strategies or inventory planning.


## 2. Common Table Expressions (CTEs)
CTEs are valuable for breaking down complicated queries into simpler, easier-to-handle parts. Let's consider an example where we use a CTE to analyze e-commerce sales by product category and region:

```sql
WITH category_sales AS (
  SELECT product_category, SUM(order_amount) AS total_sales
  FROM sales_table
  GROUP BY product_category
), region_sales AS (
  SELECT region, SUM(order_amount) AS total_sales
  FROM sales_table
  GROUP BY region
)
SELECT cs.product_category, rs.region, cs.total_sales, rs.total_sales
FROM category_sales cs
JOIN region_sales rs ON 1=1;
```

**Explanation:**
-	We create two CTEs: ‘category_sales’ calculates the total sales by product category, and ‘region_sales’ calculates the total sales by region.
-	The main query joins the CTEs based on a dummy condition (1=1) to combine the results.
-	This breakdown allows for separate analysis of sales by product category and sales by region, providing actionable insights into the performance of different product categories and regional markets.
By analyzing sales data using CTEs, Spring GDS Hong Kong can identify top-performing product categories and regions, evaluate marketing strategies, and make informed decisions about resource allocation and expansion plans.

## **Employee Sales Reporting and Trend Analysis**

CTEs allowed me to structure my queries in a more readable and manageable manner. I could create temporary result sets and call upon them multiple times within the same query. The process of debugging became less daunting, and the overall performance of my queries improved drastically.

With CTEs, here is how I tranform process to efficient pipeline:
- Identify the data requirements
- Structure the CTE
- Test each CTE for accurate results
- Combine all CTEs to generate the final output

You can use SQL to solve complicated real-world problem with 3 foundamental steps:
1. Identify the problem
2. Breakdown the pproblem in to parts for analysis
3. Gather Results and craft solutions

### **Part 1: The Problem**

Despite having a strong sales team, you've noticed an ***unsteady performance pattern in the last few quarters***.

Task: find a way to ***track your sales team's performance over time*** to ***identify the consistent high performers*** and ***those who may be facing challenges***.

### **Part 2: The Breakdown**

Now that the problem is identified and understood, let's break this down step-by-step:

1. Create a list of **each employee's total sales per quarter for the past year**.

2. Find a way to **identify the top performers for each quarter**

3. Create the employee sales trend analysis


### **Part 3: The Solution**

In this demonstration, I will create my own database. However, when solving real-world problems, please retrieve the relevant tables from the database.

**Step 1: Setup the database**
```sql

CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    role VARCHAR(50),
	hire_date DATE,
    department VARCHAR(50)
);

CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR(50),
	launch_date DATE,
    price DECIMAL(10, 2)
);

CREATE TABLE sales (
    sale_id SERIAL PRIMARY KEY,
    employee_id INT REFERENCES employees(employee_id),
    product_id INT REFERENCES products(product_id),
    sale_date DATE,
    quantity INT
);

CREATE TABLE sales_targets (
    target_id SERIAL PRIMARY KEY,
    employee_id INT REFERENCES employees(employee_id),
    quarter INT,
    year INT,
    target DECIMAL(10, 2)
);

INSERT INTO employees (first_name, last_name, role, department, hire_date)
VALUES
('Lionel', 'Messie', 'Sales Associate', 'Electronics', '2020-02-01'),
('Cristiano', 'Ranoldo', 'Sales Associate', 'Fashion', '2018-07-15'),
('Beyonc', 'Knolls', 'Sales Associate', 'Cosmetics', '2019-11-10'),
('Oprah', 'Windy', 'Sales Associate', 'Books', '2017-08-22'),
('Elon', 'Muck', 'Sales Manager', 'Electronics', '2016-06-01'),
('Steve', 'Jabs', 'Sales Manager', 'Fashion', '2015-01-01'),
('Ada', 'Lovelacer', 'Sales Manager', 'Cosmetics', '2017-03-15'),
('Marie', 'Curious', 'Sales Manager', 'Books', '2017-08-22'),
('Roger', 'Feder', 'Sales Associate', 'Sports', '2020-05-05'),
('Serena', 'Milliams', 'Sales Associate', 'Sports', '2018-12-01'),
('Tiger', 'Woodsy', 'Sales Manager', 'Sports', '2016-01-01'),
('Mick', 'Jigger', 'Sales Associate', 'Music', '2019-07-01'),
('Rihana', 'Finty', 'Sales Associate', 'Music', '2020-03-01'),
('John', 'Lennin', 'Sales Manager', 'Music', '2015-10-01'),
('Freddie', 'Mecury', 'Sales Associate', 'Home & Kitchen', '2019-09-01'),
('Cher', 'Sarkisian', 'Sales Associate', 'Home & Kitchen', '2020-11-01'),
('Gordon', 'Ramson', 'Sales Manager', 'Home & Kitchen', '2016-04-01'),
('Nelson', 'Mandel', 'Sales Associate', 'Office Supplies', '2018-10-01'),
('Mahatma', 'Ghandy', 'Sales Associate', 'Office Supplies', '2020-04-01'),
('Martin', 'Luther King', 'Sales Manager', 'Office Supplies', '2016-01-01');

INSERT INTO products (product_name, price, launch_date)
VALUES
('Galaxy Sky', 1200.00, '2020-09-01'),
('iDrone', 1500.00, '2018-11-10'),
('Zenvo Shirt', 60.00, '2017-02-20'),
('Armane Jacket', 250.00, '2018-09-15'),
('Sparkling Star Eyeshadow', 35.00, '2019-06-01'),
('Glowing Moon Lipstick', 25.00, '2020-01-15'),
('Classic tales of Mystery', 15.00, '2020-02-01'),
('Legends of the Lost City', 12.00, '2019-12-10'),
('Ace Racket', 100.00, '2020-01-10'),
('Champion Ball', 5.00, '2018-05-05'),
('Rhythm & Blues Headphones', 150.00, '2017-11-01'),
('Jazzy Beat Earbuds', 100.00, '2019-05-01'),
('Miracle Blender', 60.00, '2017-10-01'),
('Fantastic Toaster', 30.00, '2018-06-01'),
('Smooth Ink Pens', 5.00, '2020-03-01'),
('Clear Vision Paper Clips', 2.00, '2019-01-01');

INSERT INTO sales (employee_id, product_id, quantity, sale_date)
VALUES
(1, 1, 10, '2021-01-10'),
(2, 2, 5, '2021-01-15'),
(3, 3, 15, '2021-02-20'),
(4, 4, 10, '2021-02-25'),
(5, 5, 20, '2021-03-01'),
(6, 6, 15, '2021-03-10'),
(7, 7, 25, '2021-04-01'),
(8, 8, 20, '2021-04-15'),
(9, 9, 30, '2021-05-01'),
(10, 10, 25, '2021-05-10'),
(11, 11, 35, '2021-06-01'),
(12, 12, 30, '2021-06-10'),
(13, 13, 40, '2021-07-01'),
(14, 14, 35, '2021-07-10'),
(15, 15, 45, '2021-08-01'),
(16, 16, 40, '2021-08-10'),
(18, 1, 12, '2021-09-15'),
(14, 2, 18, '2021-02-18'),
(9, 3, 22, '2021-03-21'),
(20, 4, 15, '2021-12-12'),
(5, 5, 10, '2021-07-04'),
(11, 6, 20, '2021-06-15'),
(19, 7, 8, '2021-11-25'),
(2, 8, 14, '2021-05-20'),
(8, 9, 12, '2021-10-30'),
(12, 10, 9, '2021-04-11'),
(4, 11, 15, '2021-03-13'),
(6, 12, 18, '2021-08-14'),
(17, 13, 22, '2021-07-07'),
(10, 14, 12, '2021-01-20'),
(3, 15, 20, '2021-02-24'),
(7, 16, 14, '2021-05-05'),
(1, 1, 15, '2021-11-18'),
(13, 2, 8, '2021-12-28'),
(15, 3, 19, '2021-08-09'),
(16, 4, 10, '2021-07-23');


INSERT INTO sales_targets (employee_id, quarter, year, target)
VALUES
(1, 1, 2021, 500),
(1, 2, 2021, 700),
(1, 3, 2021, 800),
(1, 4, 2021, 600),
(2, 1, 2021, 550),
(2, 2, 2021, 650),
(2, 3, 2021, 750),
(2, 4, 2021, 650),
(3, 1, 2021, 600),
(3, 2, 2021, 800),
(3, 3, 2021, 850),
(3, 4, 2021, 700),
(4, 1, 2021, 580),
(4, 2, 2021, 680),
(4, 3, 2021, 780),
(4, 4, 2021, 680),
(5, 1, 2021, 630),
(5, 2, 2021, 830),
(5, 3, 2021, 880),
(5, 4, 2021, 730),
(6, 1, 2021, 600),
(6, 2, 2021, 700),
(6, 3, 2021, 800),
(6, 4, 2021, 700),
(7, 1, 2021, 620),
(7, 2, 2021, 720),
(7, 3, 2021, 820),
(7, 4, 2021, 720),
(8, 1, 2021, 650),
(8, 2, 2021, 750),
(8, 3, 2021, 850),
(8, 4, 2021, 750);

```
**Step 2: Quick analysis**

```sql
-- First, calculate the sales for each employee for the last quarter of 2021
SELECT employee_id, SUM(quantity * price) AS total_sales
FROM sales
JOIN products ON sales.product_id = products.product_id
WHERE sale_date BETWEEN '2021-10-01' AND '2021-12-31'
GROUP BY employee_id
```
**Output**

| employee_id | total_sales |
|---|---|
| 1 | 18000.00 |
| 8 | 1200.00 |
| 13 | 12000.00 |
| 19 | 120.00 |
| 20 | 3750.00 |

Next, let's turn that into a CTE so that we can perform additional analysis on it.

For example, finding the top 5 employees in terms of sales for the last quarter of 2021.

```sql
WITH sales_last_quarter AS (
    SELECT employee_id, SUM(quantity * price) AS total_sales
    FROM sales
    JOIN products ON sales.product_id = products.product_id
    WHERE sale_date BETWEEN '2021-10-01' AND '2021-12-31'
    GROUP BY employee_id
)
SELECT first_name, last_name, total_sales
FROM sales_last_quarter
JOIN employees ON sales_last_quarter.employee_id = employees.employee_id
ORDER BY total_sales DESC
LIMIT 5;
```

**Results**

| first_name | last_name | total_sales |
|---|---|---|
| Lionel | Messie | 18000.00 |
| Rihanna | Finty | 12000.00 |
| Martin | Luther King | 3750.00 |
| Marie | Curious | 1200.00 |
| Mahatma | Gandy | 120.00 |

This clause and result constitutes the base of CTE, which can be used for additional complex analysis.

**Step 3: Quarterly Employee Sales Target Performance Analysis**

With the "base CTE" created, we can perform some more complex analysis, like understanding employee sales performance vs. target on a quarterly basis.

This type of analysis solves many problems:

- It allows managers to see how many employees were able to meet their sales targets.
- This information can be used to assess the effectiveness of the sales strategies used in the last quarter.
- If the number of employees reaching their target is low, the company may need to provide additional training or resources or adjust the targets.
```sql
WITH sales_last_quarter AS (
    SELECT employee_id, SUM(quantity * price) AS total_sales
    FROM sales
    JOIN products ON sales.product_id = products.product_id
    WHERE sale_date BETWEEN '2021-10-01' AND '2021-12-31'
    GROUP BY employee_id
),
targets_last_quarter AS (
    SELECT employee_id, target
    FROM sales_targets
    WHERE quarter = 4 AND year = 2021
)
SELECT COUNT(*) as employees_reached_target
FROM sales_last_quarter
JOIN targets_last_quarter ON sales_last_quarter.employee_id = targets_last_quarter.employee_id
WHERE total_sales >= target;
```

**Results**

| employees_reached_target |
| ------------------------ |
| 2                        |

**Step 4: Employee Sales Trend Analysis: Compare Quarterly Performance vs. Annual Performance**

Finally, we can create a comparison of the quarterly sales performance against the entire year's sales performance to understand trends.

*Notice we have a new CTE that calculates the Q4 2021 targets.*

We use both CTEs to calculate the difference and then sort the results by that difference.
```sql
WITH sales_last_quarter AS (
    SELECT employee_id, SUM(quantity * price) AS total_sales
    FROM sales
    JOIN products ON sales.product_id = products.product_id
    WHERE sale_date BETWEEN '2021-10-01' AND '2021-12-31'
    GROUP BY employee_id
),
yearly_avg_sales AS (
    SELECT employee_id, AVG(quantity * price) AS avg_sales
    FROM sales
    JOIN products ON sales.product_id = products.product_id
    WHERE EXTRACT(YEAR FROM sale_date) = 2021
    GROUP BY employee_id
)
SELECT E.first_name, E.last_name, LQ.total_sales AS q4_sales, YAS.avg_sales AS yearly_avg_sales,
       (LQ.total_sales - YAS.avg_sales) / YAS.avg_sales * 100 AS percent_difference
FROM sales_last_quarter LQ
JOIN yearly_avg_sales YAS ON LQ.employee_id = YAS.employee_id
JOIN employees E ON LQ.employee_id = E.employee_id
ORDER BY percent_difference DESC;
```

**Results**

| first_name | last_name   | q4_sales | yearly_avg_sales      | percent_difference      |
| ---------- | ----------- | -------- | --------------------- | ----------------------- |
| Marie      | Curious     | 1200.00  | 720.0000000000000000  | 66.66666666666666666700 |
| Rihana     | Finty       | 12000.00 | 7200.0000000000000000 | 66.66666666666666666700 |
| Lionel     | Messie      | 18000.00 | 15000.000000000000    | 20.00000000000000000000 |
| Mahatma    | Ghandy      | 120.00   | 120.0000000000000000  | 0.00000000000000000000  |
| Martin     | Luther King | 3750.00  | 3750.0000000000000000 | 0.00000000000000000000  |

---


### Summary

1. Utilize SQL CTEs to structure and simplify complex queries.
2. Created tables, inserted data, and leveraged this data to derive meaningful insights.
3. Use CTEs to calculate total sales, analyze quarterly performance, and compare it with the yearly average for each sales representative.
4. Gained a practical understanding of how to use CTEs to identify top-performing employees and track sales trends.
5. SQL can help turn raw sales data into actionable insights that can drive business growth and inform strategic decisions.


## 3. Recursive Queries
Recursive queries can help break down complex financial data into actionable insights. Let's consider an example where we use a recursive query to calculate the cumulative revenue for each quarter:

```sql
WITH RECURSIVE quarterly_revenue AS (
  SELECT quarter, SUM(revenue) AS cumulative_revenue
  FROM financial_data
  WHERE quarter = 'Q1'
  GROUP BY quarter
  UNION ALL
  SELECT f.quarter, f.revenue + qr.cumulative_revenue
  FROM financial_data f
  JOIN quarterly_revenue qr ON f.quarter = CONCAT('Q', CAST(SUBSTRING(qr.quarter, 2) AS INT) + 1)
)
SELECT quarter, cumulative_revenue
FROM quarterly_revenue;
```

**Explanation:**
-	The initial part of the recursive CTE selects the first quarter ('Q1') and calculates the sum of revenue for that quarter.
-	The recursive part of the CTE joins the ‘financial_data’ table with the ‘quarterly_revenue’ CTE, adding the revenue of the previous quarter to the cumulative revenue.
-	The main query selects the quarter and cumulative revenue from the ‘quarterly_revenue’ CTE.
This recursive query allows a business to track the cumulative revenue for each quarter, identify revenue growth trends, and make informed decisions about budgeting, investment strategies, and resource allocation.

By utilizing these advanced SQL techniques, the business can identify trends and patterns in e-commerce sales and financial data, break down complex queries into manageable parts, and generate actionable insights. These insights can drive informed decision-making, such as adjusting marketing strategies, focusing on high-performing product categories or regions, allocating resources effectively, and setting achievable financial targets.
