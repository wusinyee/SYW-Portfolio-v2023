# Exploratory Data Analysis (EDA) on Domestic Coffee Consumption with Python 

Exploratory Data Analysis (EDA) is an essential step in any data analysis project. In this project, I will explore how to perform EDA on domestic consumption of coffee data using Python, which includes the basics of loading, cleaning, and visualizing data using Python's popular data analysis libraries, including Pandas, NumPy, Matplotlib, and seaborn. 

## 1. Importing necessary libraries:
The first step is to import the necessary libraries. We will need pandas for data manipulation, matplotlib and seaborn for data visualization, and numpy for mathematical operations.
``` python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

## 2. Loading the ddomestic consumption of coffee dataa\
Next, we load the data into a pandas DataFrame. The data is in a CSV file called "coffee_consumption.csv". You can also use pd.read_excel for Excel files, or pd.read_sql for database connections.
```python 
df = pd.read_csv('coffee_consumption.csv')
```

## 3. Exploring the Data:
The first thing to do is to explore the data to get a better understanding of its structure and content. Use the head() method to display the first few rows of the DataFrame, and the shape and info() methods to get information about the number of rows, columns, and data types.
```python
print(df.head())
print(df.shape)
print(df.info())
```

## 4. Cleaning the data
In this step, I will clean the data by removing any missing values or duplicates, and by converting any data types as necessary.
```python
# Remove rows with missing values
df.dropna(inplace=True)

# Remove duplicates
df.drop_duplicates(inplace=True)

# Convert data types
df['Date'] = pd.to_datetime(df['Date'])
```

## 5. Visualizing the Data:
Next, use various charts and plots to visualize the data. 
```python
# Line plot of coffee consumption over time
plt.figure(figsize=(10, 6))
sns.lineplot(x='Date', y='Consumption', data=df)
plt.title('Coffee Consumption Over Time')
plt.xlabel('Year')
plt.ylabel('Consumption (Millions of 60kg bags)')
plt.show()

# Histogram of coffee consumption
plt.figure(figsize=(10, 6))
sns.histplot(df['Consumption'], bins=20)
plt.title('Histogram of Coffee Consumption')
plt.xlabel('Consumption (Millions of 60kg bags)')
plt.show()

# Box plot of coffee consumption by region
plt.figure(figsize=(10, 6))
sns.boxplot(x='Region', y='Consumption', data=df)
plt.title('Coffee Consumption by Region')
plt.xlabel('Region')
plt.ylabel('Consumption (Millions of 60kg bags)')
plt.show()

# Heatmap of correlation matrix
plt.figure(figsize=(10, 6))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()
```

## 6. Analyzing the Data:
Statistical analyses will be performed on the data to gain insights into the relationships between variables. For example, we can calculate the mean, median, and standard deviation of coffee consumption, or we can use regression analysis to model the relationship between coffee consumption and other variables.
```python
# Calculate mean, median, and standard deviation of coffee consumption
print('Mean:', df['Consumption'].mean())
print('Median:', df['Consumption'].median())
print('Standard Deviation:', df['Consumption'].std())

# Perform linear regression of coffee consumption on temperature
from sklearn.linear_model import LinearRegression

X = df[['Temperature']]
y = df['Consumption']

reg = LinearRegression().fit(X, y)
print('Coefficient of Determination:', reg.score(X, y))
print('Regression Coefficients:', reg.coef_)
```
