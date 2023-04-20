# Customer Segmentation Analysis with SQL

## Project Proposal: Customer Segmentation Analysis with SQL

### Introduction
The purpose of this project is to analyze customer data and segment them into different groups based on their behavior and characteristics. This will not only help the company to target specific customer groups with personalized sales and marketing tactics, but also helps the organzation improve customer satisfaction. Better understanding of customers and knowing the pain points can generate meaningful insights on devloping a precise and coherent strategies. 

### Objectives
* To identify different customer segments based on demographics, purchasing behavior, and other characteristics
* To analyze the behavior of each segment and identify their needs and preferences
* To share the insights using tables and bulletpoints 

### Methodology
The project will be conducted using PostgreSQL relational database management system  to extract and analyze customer data. The code will be tested on an online SQL database, and posted here along with the insights. 

1. Define sample customer data schema (SQL) and create customer data table.
2. Generate sample customer data with python or mockroo.
3. Explore the customer data to identify patterns and relationships between different variables such as age, gender, location, purchase history, and preferences.
4. Use clustering techniques such as K-means clustering or hierarchical clustering to segment customers into different groups based on their behavior and characteristics.
5. Segment Analysis: Analyze the behavior of each segment by looking at their purchasing patterns, preferences, and needs.

### Deliverables:
The following deliverables are expected by the of this project:
* Self-generated CSV file with sample customer data 
* Customer data schema (SQL)
* SQL queries for customer segmentation and analysis
* Extracted insights from the analysis

### Timeline and Budget
The project will be completed with in 3 days. The data generation and ananlysis tools are free, thus this is a zero budget project.

### Conclusion
This project aims to demonstrate how to use SQL to understand customer data and present a list of queries to identify customer segments. 
TBC

---------------------------------------------------------------------------

## 1. Define sample customer data schema (SQL) and create customer data table

Befor generating the sample customer data, I defined the columns and their values as follows:

* customer_id: a string that represents the unique identifier of each customer
* first_name: a string that represents the first name of each customer
* last_name: a string that represents the last name of each customer
* email: a string that represents the email address of each customer
* age: an integer that represents the age of each customer
* gender: a string that represents the gender of each customer
* location: a string that represents the location of each customer
* education: a string that represents the education level of each customer
* income: a string that represents the income level of each customer
* channel_preference: a string that represents the channel preference of each customer
* lifecycle_stage: a string that represents the lifecycle stage of each customer
* behavior_id: an integer that represents the behavior ID of each customer
* time_spent: an integer that represents the time spent by each customer
* purchase_id: a string that represents the purchase ID of each customer
* order_date: a string that represents the date of the order
* product_category: a string that represents the product category
* brand: a string that represents the brand of the product
* order_value: a string that represents the order value
* rating: a string that represents the rating of the product
* quality: a string that represents the quality of the product
* delivery: a string that represents the delivery status of the product
* review_date: a string that represents the date of the review.

Given that all esstential data is stored in one table, I named it 'MasterCustomer' Table with the following schema (SQL):

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
    purchase_id	VARCHAR(512),
    order_date	VARCHAR(512),
    product_category	VARCHAR(512),
    brand	VARCHAR(512),
    order_value	INT,
    rating	VARCHAR(512),
    quality	VARCHAR(512),
    delivery	VARCHAR(512),
    review_date	VARCHAR(512)
);
```

I wrote INSERT statements to insert the customer data records:

```sql
INSERT INTO MasterCustomer (customer_id, first_name, last_name, email, age, gender, location, education, income, channel_preference, lifecycle_stage, behavior_id, time_spent, purchase_id, order_date, product_category, brand, order_value, rating, quality, delivery, review_date) VALUES ('L-885', 'Shaylynn', 'Klagges', 'sklagges0@yandex.ru', '81', 'Female', 'Mexico', 'High_School', '41211187', 'Email', 'New', '1', '12', 'uc757', '6/16/2021', 'Home', '"Kris, Carter and Brakus"', '44775558', '2Dissatisfied', 'Disappointing', 'Fast', '6/17/2021');
INSERT INTO MasterCustomer (customer_id, first_name, last_name, email, age, gender, location, education, income, channel_preference, lifecycle_stage, behavior_id, time_spent, purchase_id, order_date, product_category, brand, order_value, rating, quality, delivery, review_date) VALUES ('k-789', 'Maribelle', 'Di Bartolommeo', 'mdibartolommeo1@elpais.com', '46', 'Female', 'United States', 'Bachelor', '82894692', 'Mobile', 'New', '2', '17', 'SF044', '4/20/2021', 'Grocery', 'Reinger-Mann', '63655474', '1Extremely_Dissatisfied', 'Exceed_Expectation', 'Late', '4/21/2021');
```

## 2. Generate sample customer data with python or mockroo

The python script for generating 500 entries of customer data and write them into a csv file:

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


[MasterCustomer Table Schema](https://www.mockaroo.com/b002d260)


## 3. Explore the customer data to identify patterns and relationships between different variables

Customer demographics refer to the characteristics of a group of customers or the population of customers that a business serves. These characteristics may include but not limited to:
1. Age: young adults (18-35), middle-aged adults (36-60), and seniors (above 60). 
```sql
-- Query to group customers by age
SELECT
CASE
WHEN age BETWEEN 18 AND 35 THEN 'Young Adults'
WHEN age BETWEEN 36 AND 60 THEN 'Middle-Aged Adults'
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
| Middle-Aged Adults (35-60)  | 149           |
 

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

--  9.Identify the top 5 brands by number of purchases:
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
``sql
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


12. Top 5 Product Ctaegory
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




