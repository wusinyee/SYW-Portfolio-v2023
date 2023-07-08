# Other SQL Techniques for Actionable Insights in E-commerce Sales and Finance

This Markdown file serves as a reference source for SQL techniques, queries, and guides. The collection will be continuously expanding, and the content will be revised from time to time.

## Subqueries

Subqueries are queries within a query. They can be used to retrieve data from one query and use it as input for another query. Subqueries can be powerful tools for performing complex analyses and comparisons in SQL queries.

In the context of e-commerce solution sales and finance for Spring GDS Hong Kong, subqueries can help identify trends, patterns, and make informed decisions based on comparisons and calculations.

**Example:** Fetching the total revenue from e-commerce sales and comparing it with financial targets

```sql
SELECT financial_target, (SELECT SUM(revenue) FROM e-commerce_sales) AS total_revenue
FROM targets_table;
```

**Explanation:**

In this example, the main query selects the financial targets from the `targets_table`. The subquery `(SELECT SUM(revenue) FROM e-commerce_sales)` retrieves the total revenue from the `e-commerce_sales` table. The subquery is executed for each row of the main query, providing the total revenue value.

By comparing the total revenue with the financial targets, Spring GDS Hong Kong can evaluate the performance against set goals. This comparison can help identify whether the revenue aligns with the targets and make informed decisions about resource allocation, budgeting, and strategy adjustments.

**Other uses of subqueries:**

* Filtering data based on a subquery's result
* Performing calculations using subquery results
* Using subqueries in JOIN conditions

**Example:** Filtering sales data for specific products based on certain criteria

```sql
SELECT product_name, sales
FROM sales_table
WHERE product_id IN (SELECT product_id FROM product_table WHERE category = 'Electronics');
```

In this example, the subquery `(SELECT product_id FROM product_table WHERE category = 'Electronics')` retrieves the product IDs for products in the `Electronics` category. The main query then selects the product names and sales for the products that match those IDs.


## 2. Window Functions:

Window functions are functions that operate on a set of rows within a single table. Window functions can be used to calculate cumulative sums, running averages, and other aggregate functions over a sliding window of data.

In the context of e-commerce solution sales and finance for Spring GDS Hong Kong, window functions can be used to:

- Identify trends
- Calculate running totals
- Analyze data within specific partitions

**Example:** Calculating cumulative revenue using a window function

```sql
SELECT order_date, order_amount, SUM(order_amount) OVER (ORDER BY order_date) AS cumulative_revenue
FROM sales_table;
```

In this example, the query selects the order date and order amount from the `sales_table`. The window function `SUM(order_amount) OVER (ORDER BY order_date)` calculates the cumulative revenue over time. The `ORDER BY` clause specifies the order in which the rows are considered for the cumulative sum.

By using the window function, the query generates a result set that includes the cumulative revenue alongside the order date and order amount. This allows Spring GDS Hong Kong to track the growth of revenue over time, identify periods of significant increase or decrease, and analyze revenue trends.

**Window functions can be further customized by adding additional clauses such as `PARTITION BY`, `ROWS BETWEEN`, or `RANGE BETWEEN` to define the window more precisely.** 
For example, using `PARTITION BY` allows you to calculate cumulative revenue separately for each product category or region, enabling granular analysis.

```sql
SELECT order_date, order_amount, product_category, 
       SUM(order_amount) OVER (PARTITION BY product_category ORDER BY order_date) AS cumulative_revenue
FROM sales_table;
```

In this modified query, the window function `SUM(order_amount) OVER (PARTITION BY product_category ORDER BY order_date)` calculates the cumulative revenue within each product category, ordering the rows by order date.

**Window functions provide valuable insights into data patterns, trends, and comparisons within a specific context.** By utilizing window functions, Spring GDS Hong Kong can perform detailed analysis, identify growth patterns, detect outliers, and make data-driven decisions to optimize business strategies and drive success in e-commerce sales and finance.

[Another guide on window functions and CTES](https://github.com/wusinyee/SYW-Portfolio-v2023/blob/7da1a2e0886af990bcea12dae68daad3ea2a55df/Advanced%20SQL%20Techniques%20for%20Actionable%20Insights%20in%20E-commerce%20Sales%20and%20Finance.md)

3. Common Table Expressions (CTEs):
   - Example: Calculating monthly sales using a CTE and joining it with other tables
   ```sql
   WITH monthly_sales AS (
     SELECT month, SUM(sales) AS total_sales
     FROM sales_table
     GROUP BY month
   )
   SELECT ms.month, ms.total_sales, pr.profit_margin
   FROM monthly_sales ms
   JOIN profitability_table pr ON ms.month = pr.month;
   ```
   Explanation: This query creates a CTE named `monthly_sales` to calculate the total sales for each month. It then joins the CTE with the `profitability_table` to retrieve the corresponding profit margin. This allows you to analyze the relationship between sales and profitability on a monthly basis.

4. Aggregate Functions with Grouping Sets:
   - Example: Generating a sales report by product category and customer segment
   ```sql
   SELECT product_category, customer_segment, SUM(sales) AS total_sales
   FROM sales_table
   GROUP BY GROUPING SETS ((product_category), (customer_segment));
   ```
   Explanation: This query uses grouping sets to generate a comprehensive sales report that summarizes sales data by product category and customer segment. It provides insights into the performance of different categories and customer segments.

5. Advanced Join Techniques:
   - Example: Joining sales data with customer information to analyze customer behavior
   ```sql
   SELECT s.order_id, s.order_date, s.order_amount, c.customer_name
   FROM sales_table s
   INNER JOIN customer_table c ON s.customer_id = c.customer_id;
   ```
   Explanation: This query demonstrates an inner join between the `sales_table` and `customer_table` based on the customer ID. By joining these tables, you can analyze sales data alongside customer information to gain insights into customer behavior and preferences.

6. Case Statements:
   - Example: Categorizing sales data based on order amount thresholds
   ```sql
   SELECT order_id, order_amount,
          CASE
             WHEN order_amount < 1000 THEN 'Low'
             WHEN order_amount >= 1000 AND order_amount < 5000 THEN 'Medium'
             ELSE 'High'
          END AS sales_category
   FROM sales_table;
   ```
   Explanation: This query uses a case statement to categorize sales data based on different order amount thresholds. It allows you to analyze sales performance across different sales categories and identify trends within each category.

7. Temporal Queries:
   - Example: Analyzing year-over-year sales growth for a specific period
   ```sql
   SELECT year, SUM(sales) AS total_sales,
          LAG(SUM(sales)) OVER (ORDER BY year) AS previous_year_sales,
          (SUM(sales) - LAG(SUM(sales)) OVER (ORDER BY year)) / LAG(SUM(sales)) OVER (ORDER BY year) * 100 AS growth_rate
   FROM sales_table
   WHERE year BETWEEN 2020 AND 2022
   GROUP BY year;
   ```
   Explanation: This query calculates year-over-year sales growth by comparing the total sales for each year with the previous year's sales. It helps identify growth rates and trends over time.

8. Unions and Intersections:
   - Example: Consolidating sales data from multiple sources
   ```sql
   SELECT order_id, order_date, sales
   FROM sales_table_1
   UNION
   SELECT order_id, order_date, sales
   FROM sales_table_2;
   ```
   Explanation: This query combines sales data from `sales_table_1` and `sales_table_2` using the UNION operator. It consolidates sales data from different sources into a single result set for further analysis.

9. Views and Materialized Views:
   - Example: Creating a view for frequently used complex queries
   ```sql
   CREATE VIEW monthly_revenue AS
   SELECT month, SUM(revenue) AS total_revenue
   FROM sales_table
   GROUP BY month;
   ```
   Explanation: This query creates a view named `monthly_revenue` that encapsulates the query for calculating monthly revenue. It simplifies querying by allowing you to directly retrieve monthly revenue without having to rewrite the entire query.

10. Performance Optimization Techniques:
   - Example

Optimizing query performance by adding appropriate indexing to the tables involved in the query, partitioning large tables to improve data retrieval, analyzing query plans to identify and optimize performance bottlenecks, and using techniques like query rewriting or caching.

Explanation: Performance optimization is crucial for complex queries. By adding indexes, partitioning tables, and analyzing query plans, you can improve query execution time and overall database performance. Additionally, techniques like query rewriting or caching can further enhance performance by optimizing data retrieval and reducing the need for repetitive queries.

By utilizing these advanced SQL techniques in e-commerce solution sales and finance, Spring GDS Hong Kong can identify trends, patterns, and actionable insights. These techniques help break down complex queries, provide comprehensive analysis, and support informed decision-making processes.
