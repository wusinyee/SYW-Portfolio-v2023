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

| Columns             | Values         |
| ------------------- |----------------|
| customer_id         | a-000          |
| first_name          | Victor         |
| last_name           | Smith          |
| email               | xxx@xxx.com    |
| age                 | 18 to 100      |
| gender              |More than 3, very woke| 
| location            | country        |
| education           | Content Cell   |
| income              | Content Cell   |
| channel_preference  | Content Cell   |
| lifecycle_stage     | Content Cell   |
| time_spent          | Content Cell   |
| purchase_id         | Content Cell   |
| order_date          | Content Cell   |
| product_category    | Content Cell   |
| brand               | Content Cell   |
| order_value         | Content Cell   |
| rating              | Content Cell   |
| quality             | Content Cell   |
| delivery            | Content Cell   |
| review_date         | Content Cell   |


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
    income	VARCHAR(512),
    channel_preference	VARCHAR(512),
    lifecycle_stage	VARCHAR(512),
    behavior_id	INT,
    time_spent	INT,
    purchase_id	VARCHAR(512),
    order_date	VARCHAR(512),
    product_category	VARCHAR(512),
    brand	VARCHAR(512),
    order_value	VARCHAR(512),
    rating	VARCHAR(512),
    quality	VARCHAR(512),
    delivery	VARCHAR(512),
    review_date	VARCHAR(512)
);
```

I wrote INSERT statements to insert the customer data records:

```sql

INSERT INTO MasterCustomer (customer_id, first_name, last_name, email, age, gender, location, education, income, channel_preference, lifecycle_stage, behavior_id, time_spent, purchase_id, order_date, product_category, brand, order_value, rating, quality, delivery, review_date) VALUES ('d-534', 'Nadya', 'Barchrameev', 'nbarchrameev0@yellowpages.com', '75', 'Female', 'Mexico', 'Bachelor', '"$382,694.28 "', 'Social_Media', 'Active', '5', '14', 'om337', '1/4/2022', 'Computers', '"Spencer, Pouros and Lang"', '"$9,619.49 "', '5Extremely_Satisfied', 'As_Expected', 'On_time', '1/5/2022');
INSERT INTO MasterCustomer (customer_id, first_name, last_name, email, age, gender, location, education, income, channel_preference, lifecycle_stage, behavior_id, time_spent, purchase_id, order_date, product_category, brand, order_value, rating, quality, delivery, review_date) VALUES ('V-503', 'Nev', 'Purnell', 'npurnell1@skyrock.com', '32', 'Male', 'United States', 'High_School', '"$803,921.79 "', 'Mobile', 'New', '2', '12', 'L7433', '1/27/2022', 'Toys', 'Hodkiewicz-Satterfield', '"$7,998.64 "', '2Dissatisfied', 'As_Expected', 'On_time', '1/28/2022');
INSERT INTO MasterCustomer (customer_id, first_name, last_name, email, age, gender, location, education, income, channel_preference, lifecycle_stage, behavior_id, time_spent, purchase_id, order_date, product_category, brand, order_value, rating, quality, delivery, review_date) VALUES ('x-121', 'Rosamond', 'Risebarer', 'rrisebarer2@xinhuanet.com', '94', 'Female', 'United States', 'High_School', '"$350,454.18 "', 'Social_Media', 'New', '4', '17', 'cd447', '7/16/2021', 'Shoes', '"Carter, Cronin and Hintz"', '$764.74', '1Extremely_Dissatisfied', 'Exceed_Expectation', 'Fast', '7/17/2021');
INSERT INTO MasterCustomer (customer_id, first_name, last_name, email, age, gender, location, education, income, channel_preference, lifecycle_stage, behavior_id, time_spent, purchase_id, order_date, product_category, brand, order_value, rating, quality, delivery, review_date) VALUES ('2-959', 'Gannie', 'Behrendsen', 'gbehrendsen3@angelfire.com', '44', 'Male', 'Germany', 'Master', '"$697,569.86 "', 'Social_Media', 'At Risk', '3', '21', 'km529', '2/12/2022', 'Sports', 'Gutmann-Yost', '"$8,313.23 "', '4Satisfied', 'As_Expected', 'Fast', '2/13/2022');

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
1. Age: customers are grouped into 3 age groups based on their age ranges: young adults (18-35), middle-aged adults (36-60), and seniors (above 60). 

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
 




3. Gender: the gender of customers, such as male, female, or non-binary.
4. Location: the geographic location of customers, such as city, state, or country.
5. Education: the education level of customers, such as high school, college, or graduate degree.
6. Income: the income level of customers, such as low-income, middle-income, or high-income.





