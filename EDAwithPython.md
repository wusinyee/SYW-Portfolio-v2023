# Exploratory Data Analysis (EDA) on TripAdvisor Hotel Reviews 

Exploratory Data Analysis (EDA) is an essential step in any data analysis project. In this project, I will explore how to perform EDA on domestic consumption of coffee data using Python, which includes the basics of loading, cleaning, and visualizing data using Python's popular data analysis libraries, including Pandas, NumPy, Matplotlib, and seaborn. 

EDA Process Flowchat <br>
![EDAprocess drawio](https://github.com/wusinyee/SYW-Portfolio-v2023/assets/108232087/85608d10-95b3-4580-be3d-137953dc8b78)

This is a general approach to perform exploratory data analysis (EDA) on the "Trip Advisor Hotel Reviews" dataset. Here's a step-by-step guide on how you can conduct EDA:
1.	Importing necessary libraries: Start by importing the required libraries for data analysis, such as pandas, numpy, matplotlib, and seaborn. These libraries will help you manipulate and visualize the data.
2.	Loading the dataset: Use the pandas library to load the CSV file into a DataFrame. You can use the read_csv() function to accomplish this. Assign the DataFrame to a variable for further analysis.
3.	Understanding the dataset: Begin by examining the structure of the dataset. Check the number of rows and columns using the .shape attribute and display the first few rows of the DataFrame using the .head() method. This will give you an overview of the data's structure and the available columns.
4.	Data cleaning and preprocessing (if required): Depending on the dataset, you might need to perform some data cleaning steps. This can include handling missing values, converting data types, or removing irrelevant columns. Assess the dataset for any such requirements and apply the necessary data cleaning operations.
5.	Exploring the columns: Analyze each column to gain insights into the data. Calculate basic statistical measures, such as mean, median, minimum, maximum, and standard deviation, for the numeric columns. For categorical columns, determine the unique values and their frequency using the .value_counts() method. This will help you understand the distribution and characteristics of the data.
6.	Visualizing the data: Create visualizations to gain further insights into the dataset. Utilize matplotlib and seaborn to generate various plots, such as histograms, bar charts, box plots, and scatter plots. These visualizations can provide a clearer understanding of the relationships and patterns within the data.
7.	Performing sentiment analysis (if applicable): Since the dataset includes sentiment labels, you can explore the sentiment distribution. Plot the distribution of positive and negative reviews using a bar chart or pie chart. This analysis can help you understand the overall sentiment of the reviews.
8.	Analyzing ratings and reviews: Explore the relationship between ratings and reviews. You can plot a scatter plot or box plot to visualize how the ratings are distributed and if there are any patterns or correlations with the review sentiment.
9.	Analyzing hotel-specific information: Investigate specific hotel-related information. Determine the top-rated hotels based on the average ratings or the number of positive reviews. You can also analyze the distribution of reviews across different hotels.


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
