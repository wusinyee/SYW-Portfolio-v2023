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
* Self-generated CSV faile with sample customer data 
* Customer data schema (SQL)
* SQL queries for customer segmentation and analysis
* Extracted insights from the analysis

### Timeline and Budget
The project will be completed with in 3 days. The data generation and ananlysis tools are free, thus this is a zero budget project.

### Conclusion
This project aims to demonstrate how to use SQL to understand customer data and present a list of queries to identify customer segments. 
TBC

======================================================================================

## Sample Customer Data Generation

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

