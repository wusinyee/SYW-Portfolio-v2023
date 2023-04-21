# Customer Segmentation Analysis with SQL

## Project Proposal: Customer Segmentation Analysis with SQL

### Introduction
The purpose of this project is to analyze customer data and segment them into different groups based on their behavior and characteristics. The objective is to help the company target specific customer groups with personalized sales and marketing tactics, improve customer satisfaction, and develop precise and coherent strategies to meet their needs. 
**Initially, the project did not involve the development of strategies. However, without taking action on the insights gained from the analysis, the purpose of conducting the analysis would be defeated**

### Objectives
* To identify different customer segments based on demographics, purchasing behavior, and other characteristics.
* To analyze the behavior of each segment and identify their needs and preferences
* To evaluate the performance of clustering techniques by using appropriate metrics.
* To share the insights in a clear and concise manner

### Methodology
The project will be conducted using PostgreSQL relational database management system to extract and analyze customer data. The following steps will be taken:
1. Define the scope and limitations of the project, including the types of data that will be analyzed and the time period covered
2. Verify the quality of data, ensure it is ready for analysis
3. Generate sample customer data with Python or Mockaroo
4. Explore the customer data to identify patterns and relationships between different variables
5. Analyze the behavior of each segment by looking at their purchasing patterns, preferences, and needs
6. Share the insights gained from the analysis using tables and bullet points
7. Formulate strategies to maximize sales and recommend effective tactics based on the insights

### Deliverables:
The following deliverables are expected by the end of this project:
* [Effective Tactics and strategies to maximize sales](https://github.com/wusinyee/SYW-Portfolio-v2023/blob/main/Customer%20Segmentation%20Analysis%20with%20SQL.md#7-formulate-strategies-to-maximize-sales-and-recommend-effective-tactics-based-on-the-insights)
* [SQL queries for customer segmentation analysis](https://github.com/wusinyee/SYW-Portfolio-v2023/blob/main/Customer%20Segmentation%20Analysis%20with%20SQL.md#4-explore-the-customer-data-to-identify-patterns-and-relationships-between-different-variables)
* [Extracted insights from the analysis](https://github.com/wusinyee/SYW-Portfolio-v2023/edit/main/Customer%20Segmentation%20Analysis%20with%20SQL.md#6-share-the-insights-gained-from-the-analysis-using-tables-and-bullet-points)

### Timeline and Budget
This project will be completed within 3 days, before 22 April. The data generation and analysis tools are free, so the budget for this project is zero.

---------------------------------------------------------------------------

## 1. Define the scope and limitations of the project

**Scope**: 
- The project aims to analyze customer data and segment them into different groups based on their behavior and characteristics, using SQL queries
- The project will use two tables: MasterCustomer and Purchases, generated with mockaroo.com
- The analysis will focus on identifying patterns and relationships between different variables such as demographics, purchasing behavior, and preferences
- The project will use clustering techniques such as K-means clustering or hierarchical clustering to segment customers into different groups
- The project will evaluate the performance of clustering techniques using appropriate metrics such as silhouette score or elbow method to determine the optimal number of clusters
- The project will present the insights gained from the analysis using tables, graphs, and bullet points

The Schema for the two main sources of customer data:
```sql
CREATE TABLE MasterCustomer 
(
    customer_id	VARCHAR(512),
    first_name	VARCHAR(512),
    last_name	VARCHAR(512),
    email	VARCHAR(512),
    age	INT,
    gender	VARCHAR(512),
    location	VARCHAR(512),
    education	VARCHAR(512),
    income	INT,
    channel_preference	VARCHAR(512),
    lifecycle_stage	VARCHAR(512),
    behavior_id	INT,
    time_spent	INT,
    order_date	VARCHAR(512),
    product_category	VARCHAR(512),
    brand	VARCHAR(512),
    order_value	INT,
    rating	VARCHAR(512),
    quality	VARCHAR(512),
    delivery	VARCHAR(512),
    review_date	VARCHAR(512)
);

CREATE TABLE Purchases 
(
    customer_id	VARCHAR(512),
    purchase_id	VARCHAR(512),
    first_name	VARCHAR(512),
    last_name	VARCHAR(512),
    gender	VARCHAR(512),
    location	VARCHAR(512),
    education	VARCHAR(512),
    income	INT,
    channel_preference	VARCHAR(512),
    lifecycle_stage	VARCHAR(512),
    behavior_id	INT,
    time_spent	INT,
    order_date	VARCHAR(512),
    product_category	VARCHAR(512),
    brand	VARCHAR(512),
    order_value	INT,
    order_frequency	INT,
    total_num_purchase	VARCHAR(512),
    total_num_purchase2	INT,
    quantity	INT,
    Price	INT
);
```
The code above defines two database tables, "MasterCustomer" and "Purchases":
* "MasterCustomer" table includes columns for various customer information, such as their ID, first and last name, email, age, gender, location, education, income, channel preference, lifecycle stage, behavior ID, time spent, order date, product category, brand, order value, rating, quality, delivery, and review date. 
* These columns are defined with specific data types, such as VARCHAR (variable-length character string) and INT (integer).
* "Purchases" table includes columns for customer and purchase information, such as the customer ID, purchase ID, first and last name, gender, location, education, income, channel preference, lifecycle stage, behavior ID, time spent, order date, product category, brand, order value, order frequency, total number of purchases, total number of purchases (in integer format), quantity, and price. These columns are also defined with specific data types.
* These two tables store information related to customer demographics, behavior, and purchasing history, which can be used for analysis and decision-making purposes

**Limitations**
- The project only uses simulated customer data generated by mockaroo.com, which may not accurately represent real-world customer behavior
- The project only uses SQL queries for data analysis, which may not be sufficient to capture the full complexity of customer behavior and preferences
- The project will not provide any specific recommendations for how the company should act on the insights gained from the analysis

## 2. Verify the quality of data, ensure it is ready for analysis

You may use python script for generating 500 entries of customer data and write them into a csv file:

```python

import random
import csv
import datetime

# list of possible values for each column
first_names = ["John", "Jane", "Tom", "Sara", "Mike", "Barry"]
last_names = ["Doe", "Smith", "Brown", "Johnson", "Williams"]
domains = ["example.com", "test.com", "sample.com"]
genders = ["Male", "Female"]
locations = ["New York", "Los Angeles", "Chicago", "Miami", "San Francisco"]
education_levels = ["Bachelor", "Master", "PhD"]
channel_preferences = ["Email", "Social Media", "Mobile"]
lifecycle_stages = ["Active", "At Risk", "New"]
product_categories = ["Electronics", "Fashion", "Beauty", "Sports", "Books"]
brands = ["Apple", "Nike", "Adidas", "Samsung", "Amazon"]
ratings = ["1", "2", "3", "4", "5"]
qualities = ["Low", "Medium", "High"]
deliveries = ["Fast", "Normal", "Slow"]

# open a new CSV file and write headers
with open("customer_data.csv", mode="w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["first_name", "last_name", "email", "age", "gender", "location", "education",
                     "income", "channel_preference", "lifecycle_stage", "behavior_id", "time_spent",
                     "purchase_id", "order_date", "product_category", "brand", "order_value",
                     "rating", "quality", "delivery", "review_date"])

    # generate 500 random entries
    for i in range(500):
        # generate random values for each column
        first_name = random.choice(first_names)
        last_name = random.choice(last_names)
        email = f"{first_name.lower()}.{last_name.lower()}@{random.choice(domains)}"
        age = random.randint(18, 65)
        gender = random.choice(genders)
        location = random.choice(locations)
        education = random.choice(education_levels)
        income = random.randint(20000, 150000)
        channel_preference = random.choice(channel_preferences)
        lifecycle_stage = random.choice(lifecycle_stages)
        behavior_id = f"Behavior-{i+1}"
        time_spent = random.randint(10, 120)
        purchase_id = f"Order-{i+1}"
        order_date = datetime.date.today() - datetime.timedelta(days=random.randint(1, 30))
        product_category = random.choice(product_categories)
        brand = random.choice(brands)
        order_value = random.randint(10, 500)
        rating = random.choice(ratings)
        quality = random.choice(qualities)
        delivery = random.choice(deliveries)
        review_date = datetime.date.today() - datetime.timedelta(days=random.randint(1, 60))

        # write the row to the CSV file
        writer.writerow([first_name, last_name, email, age, gender, location, education,
                         income, channel_preference, lifecycle_stage, behavior_id, time_spent,
                         purchase_id, order_date, product_category, brand, order_value,
                         rating, quality, delivery, review_date])

print("Customer data generated successfully!")
```
## 3. Generate sample customer data with Python or Mockaroo

[MasterCustomer Table Schema](https://www.mockaroo.com/b002d260)
![Preview of the data, both tables are prepared to be analyzed](https://github.com/wusinyee/SYW-Portfolio-v2023/blob/5e659e77c0dec711ee8b30ca81ce51720cfb50b7/snapshot.png)


## 4. Explore the customer data to identify patterns and relationships between different variables

Customer demographics refer to the characteristics of a group of customers or the population of customers that a business serves.
1. Age: young adults (18-35), middle age adults (36-60), and seniors (above 60). 
```sql
-- Query to group customers by age
SELECT
CASE
WHEN age BETWEEN 18 AND 35 THEN 'Young Adults'
WHEN age BETWEEN 36 AND 60 THEN 'Middle Age Adults'
WHEN age > 60 THEN 'Seniors'
END AS age_group,
COUNT(*) as num_customers
FROM MasterCustomer
GROUP BY age_group;
```
To group customers by age as young adults, middle-aged adults, and seniors, I used the CASE statement in SQL to create age ranges and group customers based on those ranges. 

| age_group                   | num_customers |
| --------------------------  | ------------- |
| Seniors (above 60)          | 250           |
| Young Adults (18-35)        | 101           |
| Middle Age Adults (35-60)  | 149           |
 

2. Gender: the 8 genders of customers.
```sql
    SELECT gender, COUNT(*) as num_customers
    FROM MasterCustomer
    GROUP BY gender;
   ```
| gender       | num_customers |
| ------------ | ------------- |
| Male         | 215           |
| Non-binary   | 6             |
| Genderqueer  | 8             |
| Bigender     | 6             |
| Genderfluid  | 8             |
| Polygender   | 13            |
| Female       | 237           |
| Agender      | 7             |


3. Location: the geographic location of customers, such as city, state, or country.
```sql
    SELECT location, COUNT(*) as num_customers
    FROM MasterCustomer
    GROUP BY location;
```

| location        | num_customers |
| --------------- | ------------- |
| United Kingdom  | 23            |
| Netherlands     | 39            |
| Mexico          | 130           |
| Germany         | 42            |
| United States   | 266           |


4. Education: the education level of customers, such as high school, college, or graduate degree.
```sql
    SELECT education, COUNT(*) as num_customers
    FROM MasterCustomer
    GROUP BY education;
```

| education    | num_customers |
| -------------| ------------- |
| PHD          | 115           |
| Master       | 122           |
| Bachelor     | 141           |
| High_School  | 122           |
   

5. Income: the income level of customers, such as low-income, middle-income, or high-income.
```sql
SELECT 
    CASE 
        WHEN income < 1000000 THEN 'Low Income'
        WHEN income >= 1000000 AND income < 2800000 THEN 'Middle-Class'
        WHEN income >= 2800000 AND income < 3500000 THEN 'Upper Middle-Class'
        ELSE 'High Income'
    END AS income_group,
    COUNT(*) AS customer_count
FROM MasterCustomer
GROUP BY income_group;
```
| income_group        | customer_count |
| ------------------- | -------------- |
| High Income         | 483            |
| Upper Middle-Class  | 3              |
| Middle-Class        | 11             |
| Low Income          | 3              |

6. Identify the number of customers by channel preference:
```sql
    SELECT channel_preference, COUNT(*) as num_customers
    FROM MasterCustomer
    GROUP BY channel_preference
    ORDER BY num_customers DESC;
```
| channel_preference | num_customers |
| ------------------ | ------------- |
| Email              | 185           |
| Mobile             | 176           |
| Social_Media       | 139           |

7. Identify the average time spent on the website by lifecycle stage:
```sql
    SELECT lifecycle_stage, AVG(time_spent) as avg_time_spent
    FROM MasterCustomer
    GROUP BY lifecycle_stage;
```
| lifecycle_stage | avg_time_spent      |
| --------------- | ------------------- |
| New             | 13.6390532544378698 |
| Active          | 12.1944444444444444 |
| At Risk         | 12.5231788079470199 |

--  8. Identify the top 5 product categories by order value: 
```sql
    SELECT product_category, SUM(order_value) AS total_order_value
    FROM MasterCustomer
    GROUP BY product_category
    ORDER BY total_order_value DESC
    LIMIT 5;
```
| product_category | total_order_value |
| ---------------- | ----------------- |
| Outdoors         | 1736513919        |
| Toys             | 1513426403        |
| Health           | 1348957645        |
| Home             | 1339721128        |
| Industrial       | 1328806015        |

9.Identify the top 5 brands by number of purchases:
```sql
    SELECT brand, COUNT(*) as num_purchases
    FROM MasterCustomer
    GROUP BY brand
    ORDER BY num_purchases DESC
    LIMIT 5;
```
| brand                         | num_purchases |
| ----------------------------- | ------------- |
| "Rohan, Hudson and Gulgowski" | 1             |
| Wolf-Kutch                    | 1             |
| Dare-Wiegand                  | 1             |
| Cole-Ruecker                  | 1             |
| Abshire-Pacocha               | 1             |

10. Identify the average order value by rating:
```sql
    SELECT rating, AVG(CAST(order_value AS INT)) as avg_order_value
    FROM MasterCustomer
    GROUP BY rating;
```
| rating                  | avg_order_value       |
| ----------------------- | --------------------- |
| 4Satisfied              | 44178787.535714285714 |
| 5Extremely_Satisfied    | 49236718.173913043478 |
| 1Extremely_Dissatisfied | 47575404.910000000000 |
| 3Neutral                | 47331447.305263157895 |
| 2Dissatisfied           | 46725728.910891089109 |

Ad hoc analysis from average order value by rating:
* The highest average order value is associated with the customers who are "Extremely Satisfied" (rating 5) with an average order value of $49,236,718. This could imply that customers who have a better experience tend to spend more
* The lowest average order value is associated with the customers who are "Dissatisfied" (rating 2) with an average order value of $46,725,728. This suggests that customers who have a poor experience tend to spend less
* The difference in average order value between the most satisfied and least satisfied customers is around $3 million. This indicates that customer satisfaction could have a significant impact on overall sales
* The customers who are "Satisfied" (rating 4) and "Extremely Satisfied" (rating 5) have higher average order values compared to those who are "Dissatisfied" (rating 2) and "Extremely Dissatisfied" (rating 1). This suggests that a better customer experience can lead to higher spending.
* The customers who are "Neutral" (rating 3) have a slightly lower average order value compared to the "Satisfied" (rating 4) and "Extremely Satisfied" (rating 5) customers. This could imply that simply satisfying the customers may not be enough to encourage higher spending, and businesses may need to strive for a better experience to drive sales.

11. Top 10  Valuable Customers
```sql
    SELECT 
        mc.customer_id, 
        mc.first_name, 
        mc.last_name, 
        SUM(p.order_value) AS total_spending, 
        COUNT(DISTINCT p.purchase_id) AS total_orders 
    FROM 
        MasterCustomer mc 
        INNER JOIN Purchases p ON mc.customer_id = p.customer_id 
    GROUP BY 
        mc.customer_id, 
        mc.first_name, 
        mc.last_name 
    ORDER BY 
        total_spending DESC, 
        total_orders DESC 
    LIMIT 
        10;
 ```

| customer_id | first_name | last_name   | total_spending | total_orders |
| ----------- | ---------- | ----------- | -------------- | ------------ |
| e-745       | Wang       | Grzeszczak  | 140646994      | 2            |
| e-745       | Cristen    | Block       | 140646994      | 2            |
| 6-111       | Marylynne  | Sulman      | 99869951       | 1            |
| n-065       | Giana      | Prout       | 99809945       | 1            |
| d-658       | Blondell   | Betteney    | 99689586       | 1            |
| e-285       | Phebe      | Henrionot   | 99213308       | 1            |
| E-789       | Bartie     | Postlewhite | 99032798       | 1            |
| 7-661       | Steve      | Lockery     | 98426506       | 1            |
| H-391       | Kelley     | Stoad       | 98395749       | 1            |
| y-057       | Ruperta    | Davidde     | 98210904       | 1            |


12. Top 3 Product Ctaegory
```sql
    SELECT product_category, COUNT(*) AS num_purchases
    FROM Purchases
    GROUP BY product_category
    ORDER BY num_purchases DESC
    LIMIT 3;
```
| product_category | num_purchases |
| ---------------- | ------------- |
| Outdoors         | 33            |
| Industrial       | 29            |
| Health           | 29            |

13. Age group that spends the most
 ```sql
 SELECT 
        CASE 
            WHEN age BETWEEN 18 AND 35 THEN 'Young Adults'
            WHEN age BETWEEN 36 AND 60 THEN 'Middle-Aged Adults'
            ELSE 'Seniors'
        END AS age_group,
        SUM(Purchases.order_value) AS total_spending
    FROM 
        MasterCustomer 
        JOIN Purchases ON MasterCustomer.customer_id = Purchases.customer_id
    
    GROUP BY 
        age_group
    ORDER BY 
        total_spending DESC;
```

| age_group          | total_spending |
| ------------------ | -------------- |
| Seniors            | 11483313571    |
| Middle-Aged Adults | 6801382310     |
| Young Adults       | 5307079994     |

14. Profitability by Locations
```sql
    SELECT 
        mc.location,
        SUM(p.order_value) AS total_spending
    FROM 
        MasterCustomer mc
        JOIN Purchases p ON mc.customer_id = p.customer_id
    GROUP BY 
        mc.location
    ORDER BY 
        total_spending DESC 
    LIMIT 1;
```

| location      | total_spending |
| ------------- | -------------- |
| United States | 11796352053    |

## 5. Analyze the behavior of each segment
 
I filtered a series of queries that could help me obtain valuable insights from the customer data and contribute to a data-driven sales and marketing strategy.

## 6. Share the insights gained from the analysis using tables and bullet points

Insight 1:  Identify the most valuable customers (Top 10)
```sql
   SELECT 
        mc.customer_id, 
        mc.first_name, 
        mc.last_name, 
        SUM(p.order_value) AS total_spending, 
        COUNT(DISTINCT p.purchase_id) AS total_orders 
    FROM 
        MasterCustomer mc 
        INNER JOIN Purchases p ON mc.customer_id = p.customer_id 
    GROUP BY 
        mc.customer_id, 
        mc.first_name, 
        mc.last_name 
    ORDER BY 
        total_spending DESC, 
        total_orders DESC 
    LIMIT 
        10;
```
This query identifies the customers who have spent the most money and made the most orders. 

| customer_id | first_name | last_name   | total_spending | total_orders |
| ----------- | ---------- | ----------- | -------------- | ------------ |
| e-745       | Wang       | Grzeszczak  | 140646994      | 2            |
| e-745       | Cristen    | Block       | 140646994      | 2            |
| 6-111       | Marylynne  | Sulman      | 99869951       | 1            |
| n-065       | Giana      | Prout       | 99809945       | 1            |
| d-658       | Blondell   | Betteney    | 99689586       | 1            |
| e-285       | Phebe      | Henrionot   | 99213308       | 1            |
| E-789       | Bartie     | Postlewhite | 99032798       | 1            |
| 7-661       | Steve      | Lockery     | 98426506       | 1            |
| H-391       | Kelley     | Stoad       | 98395749       | 1            |
| y-057       | Ruperta    | Davidde     | 98210904       | 1            |

This information can be used to target these customers with personalized marketing campaigns, loyalty programs, and upsell opportunities.
* The top two rows show that customers with the rating "Satisfied" and "Extremely_Satisfied" have a higher average order value compared to other ratings
* The customer with customer_id "e-745" has the highest total spending of 140646994 and has placed 2 orders
* Most customers have made only 1 order, with only two customers having placed more than one order.

Insight 2. Determine the most popular product categories (Top 3)
```sql
SELECT product_category, COUNT(*) AS num_purchases
    FROM Purchases
    GROUP BY product_category
    ORDER BY num_purchases DESC
    LIMIT 3;
 ```
This query pinpoits the most popular product categories among your customers. 

| product_category | num_purchases |
| ---------------- | ------------- |
| Outdoors         | 33            |
| Industrial       | 29            |
| Health           | 29            |

These insights optimizes product offerings and marketing campaigns, and potentially expand the product line to capitalize on the most in-demand categories.
* The top product categories based on the number of purchases are Outdoors, Industrial, and Health
* Customers with customer_id e-745 and total_spending of 140646994 have made 2 orders, making them the highest spenders in the given data
* Majority of the customers have made only one order, except for the customer with customer_id e-745 and Cristen Block
* Customers with age under 30 have the highest average order value compared to other age groups

Insight 3. Analyze customer behavior by channel preference
```sql
SELECT 
    MasterCustomer.channel_preference, 
    AVG(Purchases.order_value) AS avg_order_value, 
    COUNT(DISTINCT MasterCustomer.customer_id) AS num_customers
FROM 
    MasterCustomer 
    JOIN Purchases USING (customer_id)
GROUP BY 
    MasterCustomer.channel_preference;
```
This query demonstrates which channels the customers prefer to use when making purchases, and how their spending behavior differs across those channels. 

| channel_preference | avg_order_value       | num_customers |
| ------------------ | --------------------- | ------------- |
| Email              | 46691840.612903225806 | 185           |
| Mobile             | 46795553.517045454545 | 176           |
| Social_Media       | 47650543.585714285714 | 139           |

This information can to optimize  marketing campaigns for each channel, and potentially invest more in the channels that are most popular among the customers.
* Customers who prefer to purchase through Social Media have a higher average order value than those who prefer Email and Mobile, but the number of customers who prefer Social Media is the lowest among the three channels

Insight 4. Segment customers by demographic and behavior
```sql
SELECT 
    CASE 
        WHEN age < 30 THEN 'Under 30'
        WHEN age >= 30 AND age < 50 THEN '30-50'
        ELSE '50 and over'
    END AS age_group, 
    MasterCustomer.gender, 
    MasterCustomer.education, 
    AVG(Purchases.order_value) AS avg_order_value,
    COUNT(DISTINCT MasterCustomer.customer_id) AS num_customers
FROM 
    MasterCustomer 
    JOIN Purchases USING (customer_id)
GROUP BY 
    age_group, 
    MasterCustomer.gender, 
    MasterCustomer.education;
```

This query segments the customers by demographic and spending behavior. 

| age_group   | gender      | education   | avg_order_value       | num_customers |
| ----------- | ----------- | ----------- | --------------------- | ------------- |
| 30-50       | Agender     | High_School | 92039087.000000000000 | 1             |
| 30-50       | Bigender    | Master      | 75000507.000000000000 | 1             |
| 30-50       | Female      | Bachelor    | 56278815.928571428571 | 14            |
| 30-50       | Female      | High_School | 52655015.416666666667 | 12            |
| 30-50       | Female      | Master      | 42093121.285714285714 | 14            |
| 30-50       | Female      | PHD         | 42686069.214285714286 | 14            |
| 30-50       | Genderfluid | High_School | 20738004.000000000000 | 1             |
| 30-50       | Genderfluid | Master      | 70397696.000000000000 | 1             |
| 30-50       | Genderfluid | PHD         | 63140865.000000000000 | 1             |
| 30-50       | Genderqueer | Bachelor    | 85303260.000000000000 | 1             |
| 30-50       | Genderqueer | High_School | 70185565.000000000000 | 1             |
| 30-50       | Genderqueer | Master      | 34828595.000000000000 | 1             |
| 30-50       | Male        | Bachelor    | 41984286.166666666667 | 12            |
| 30-50       | Male        | High_School | 45634881.157894736842 | 19            |
| 30-50       | Male        | Master      | 64809057.250000000000 | 11            |
| 30-50       | Male        | PHD         | 52661921.750000000000 | 16            |
| 30-50       | Non-binary  | High_School | 29317160.000000000000 | 1             |
| 30-50       | Polygender  | Bachelor    | 24341811.500000000000 | 2             |
| 30-50       | Polygender  | Master      | 41823470.500000000000 | 2             |
| 50 and over | Agender     | Bachelor    | 78293480.000000000000 | 1             |
| 50 and over | Agender     | High_School | 52165786.000000000000 | 2             |
| 50 and over | Agender     | Master      | 38484430.000000000000 | 1             |
| 50 and over | Bigender    | High_School | 57443391.000000000000 | 3             |
| 50 and over | Bigender    | Master      | 10036459.000000000000 | 1             |
| 50 and over | Female      | Bachelor    | 42954426.756756756757 | 37            |
| 50 and over | Female      | High_School | 40029194.852941176471 | 34            |
| 50 and over | Female      | Master      | 47902892.050000000000 | 19            |
| 50 and over | Female      | PHD         | 40735117.205882352941 | 34            |
| 50 and over | Genderfluid | Bachelor    | 31368503.000000000000 | 2             |
| 50 and over | Genderfluid | High_School | 56112954.000000000000 | 1             |
| 50 and over | Genderfluid | Master      | 33622911.500000000000 | 2             |
| 50 and over | Genderfluid | PHD         | 18156675.000000000000 | 1             |
| 50 and over | Genderqueer | Bachelor    | 32310220.000000000000 | 2             |
| 50 and over | Genderqueer | High_School | 22932831.000000000000 | 1             |
| 50 and over | Genderqueer | Master      | 70974500.500000000000 | 2             |
| 50 and over | Male        | Bachelor    | 54057420.885714285714 | 35            |
| 50 and over | Male        | High_School | 41998126.224489795918 | 49            |
| 50 and over | Male        | Master      | 51909845.352941176471 | 34            |
| 50 and over | Male        | PHD         | 50277864.800000000000 | 25            |
| 50 and over | Non-binary  | Bachelor    | 95917990.000000000000 | 1             |
| 50 and over | Non-binary  | High_School | 377669.000000000000   | 1             |
| 50 and over | Non-binary  | Master      | 48637115.500000000000 | 2             |
| 50 and over | Non-binary  | PHD         | 35442358.000000000000 | 2             |
| 50 and over | Polygender  | High_School | 71470664.666666666667 | 3             |
| 50 and over | Polygender  | Master      | 52981772.000000000000 | 1             |
| Under 30    | Female      | Bachelor    | 44911533.125000000000 | 16            |
| Under 30    | Female      | High_School | 48608585.538461538462 | 13            |
| Under 30    | Female      | Master      | 44000902.000000000000 | 8             |
| Under 30    | Female      | PHD         | 53049145.416666666667 | 12            |
| Under 30    | Genderfluid | Master      | 20248760.000000000000 | 1             |
| Under 30    | Genderqueer | High_School | 66913874.000000000000 | 1             |
| Under 30    | Genderqueer | PHD         | 40231021.000000000000 | 1             |
| Under 30    | Male        | Bachelor    | 47450889.888888888889 | 9             |
| Under 30    | Male        | High_School | 62260482.142857142857 | 7             |
| Under 30    | Male        | Master      | 31666352.571428571429 | 7             |
| Under 30    | Male        | PHD         | 24720427.333333333333 | 3             |
| Under 30    | Non-binary  | High_School | 61218059.000000000000 | 1             |

These inisghts contribute to targeted marketing campaigns for each segment, tailoring messaging and promotions to the specific interests and preferences of each group.
* The average order value of customers aged 30-50 is higher than that of customers aged 50 and over
* Male customers have the highest average order value across all education levels in both age groups
* Female customers aged 50 and over have the highest number of customers
* There are very few customers who identify as genderqueer, genderfluid, agender, non-binary, bigender or polygender, regardless of age and education level
* Customers with a bachelor's degree have a higher average order value compared to those with a high school diploma or a master's degree. However, customers with a PhD have a higher average order value compared to those with a bachelor's degree or a master's degree, particularly in the 30-50 age group
* The highest average order value for customers with a PhD in the 30-50 age group is from those who identify as genderfluid

5. Analyze customer churn:
```sql
SELECT 
    COUNT(DISTINCT customer_id) AS num_churned_customers
FROM 
    MasterCustomer 
WHERE 
    customer_id NOT IN (
        SELECT DISTINCT customer_id FROM Purchases 
        WHERE order_date >= '2022-01-01' AND order_date <= '2022-12-31'
    )
```
This query identifies the number of customers who have stopped ordering over a specific time period. This insight leads to the reasons why these customers left and take steps to improve customer experience, potentially implementing retention campaigns to try and win back lost customers.

## 7. Formulate strategies to maximize sales and recommend effective tactics based on the insights

### Strategies to maximize sales:
* Focus on the 30-50 group as they have the highest average order value
* Target customers with higher education levels, such as Master's and PhD holders, as they tend to have a higher average order value
* Increase marketing efforts towards female customers, who make up the majority of the customer base and have a relatively high average order value
* Develop marketing campaigns specifically targeted towards non-binary and genderqueer customers, who currently have a smaller customer base but a higher average order value
* Consider offering promotions or discounts to customers who have a lower average order value, such as those with a high school education or those in the 50 and over age group
* Look for opportunities to upsell or cross-sell to existing customers, as this can increase the average order value and overall revenue
* Continuously monitor and analyze customer data to identify patterns and trends, and adjust marketing and sales strategies accordingly

### Effective tactics to maximize sales
* Offer promotions and discounts: Customers love a good deal. Offer discounts, BOGO deals, or other promotions to entice them to make a purchase
* Improve the checkout process: Make sure the checkout process is as smooth and easy as possible
* Remove any unnecessary steps, offer multiple payment options, and provide clear instructions to reduce cart abandonment
* Leverage social media: Use social media platforms like Facebook, Instagram, and Twitter to promote your products and engage with customers. Run ads and share user-generated content to increase brand awareness
* Provide high quality customer service: Respond to customer inquiries and complaints promptly and professionally. Go above and beyond to ensure customer satisfaction, as happy customers are more likely to make repeat purchases
* Use email marketing: Send out newsletters and promotional emails to keep customers informed about new products, discounts, and other news related to your business.
* Upsell and cross-sell: Offer related products or upgrades during the checkout process to increase the average order value.
* SEO: Use keywords and meta tags to improve your website's visibility on search engines like Google, making it easier for potential customers to find you


## Conclusion

This project aims to demonstrate how to use SQL to understand customer data and present a list of queries to identify customer segments. By identifying different customer segments based on demographics, purchasing behavior, and other characteristics, the company can better tailor its marketing strategies and improve customer satisfaction.
