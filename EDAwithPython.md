# Exploratory Data Analysis (EDA) on Domestic Coffee Consumption with Python 

Exploratory Data Analysis (EDA) is an essential step in any data analysis project. In this project, I will explore how to perform EDA on domestic consumption of coffee data using Python, which includes the basics of loading, cleaning, and visualizing data using Python's popular data analysis libraries, including Pandas, NumPy, Matplotlib, and seaborn. 

EDA Process Flowchat <br>
![EDAprocess drawio](https://github.com/wusinyee/SYW-Portfolio-v2023/assets/108232087/85608d10-95b3-4580-be3d-137953dc8b78)

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Step 1: Import necessary libraries

# Step 2: Load the dataset
df = pd.read_csv('tripadvisor_hotel_reviews.csv')

# Step 3: Understanding the dataset
print("Shape of the dataset:", df.shape)
print("First few rows of the dataset:")
print(df.head())

# Step 4: Data cleaning and preprocessing (if required)
# Perform any necessary data cleaning steps here

# Step 5: Exploring the columns
print("Summary statistics for numeric columns:")
print(df.describe())

print("Unique values in the 'Rating' column:")
print(df['Rating'].value_counts())

# Step 6: Visualizing the data
plt.figure(figsize=(10, 6))
sns.histplot(df['Rating'], bins=5, kde=True)
plt.xlabel('Rating')
plt.ylabel('Count')
plt.title('Distribution of Ratings')
plt.show()

# Step 7: Performing sentiment analysis
plt.figure(figsize=(6, 6))
df['Sentiment'].value_counts().plot(kind='pie', autopct='%1.1f%%')
plt.title('Sentiment Distribution')
plt.show()

# Step 8: Analyzing ratings and reviews
plt.figure(figsize=(10, 6))
sns.boxplot(x='Rating', y='Review', data=df)
plt.xlabel('Rating')
plt.ylabel('Review')
plt.title('Ratings vs Reviews')
plt.show()

# Step 9: Analyzing hotel-specific information
top_rated_hotels = df.groupby('Hotel_Name')['Rating'].mean().nlargest(10)
print("Top 10 highest rated hotels:")
print(top_rated_hotels)

# Step 10: Temporal analysis (if applicable)
# If the dataset includes review dates, you can perform temporal analysis here
```
