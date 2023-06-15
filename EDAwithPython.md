# Exploratory Data Analysis (EDA) on Dairy Products Dataset using Python

## Introduction
Exploratory Data Analysis (EDA) is an essential step in any data analysis project. Exploratory data analysis (EDA) allows us to gain valuable insights into dairy products, such as their qualities, nutritional content, and customer feedback. By analyzing a dataset containing information about various dairy products, we can obtain perspective from the data set's big picture, then understand their composition, pricing, and consumer preferences.

The dataset includes both numerical and categorical variables, such as product type, fat content, price, weight, calories, protein content, calcium content, sodium content, carbohydrates, sugar content, cholesterol content, and customer ratings. These variables provide a comprehensive view of the dairy products and help us uncover patterns and distributions.

The EDA process involves loading the dataset, examining its structure, checking for missing values, and generating summary statistics. We then look into individual variables for revealing insights and explore relationships between variables. In addition, we will handle any missing values or outliers encountered during the analysis. We will use [Python code](https://github.com/wusinyee/SYW-Portfolio-v2023/blob/main/EDAwithPython.md#source-code-) to perform the EDA.

The outcomes of this EDA have major implications for dairy industry stakeholders such as producers, marketers, and consumers. In a competitive market, the insights gained can help with informed decision-making and efficiency optimization.


### EDA Process Flowchat <br>
![EDAprocess drawio](https://github.com/wusinyee/SYW-Portfolio-v2023/assets/108232087/85608d10-95b3-4580-be3d-137953dc8b78)

## A systematic guide on performing EDA  <br>

1.	Importing Libraries:
* The code begins by importing the necessary libraries: pandas, numpy, matplotlib.pyplot, and seaborn. These libraries are commonly used for data analysis and visualization in Python.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

2.	Loading the Dataset:
* The dataset is loaded into a DataFrame using the pd.read_csv() function.

```python
df = pd.read_csv('dairy_products_dataset.csv')
```

3.	Understanding the Dataset:
*	The code provides an overview of the dataset:
*	It prints the number of rows and columns in the dataset using the shape attribute of the DataFrame.
*	It displays the data types of each column using the dtypes attribute of the DataFrame.
*	It presents the summary statistics of the numerical columns using the describe() method of the DataFrame.

```python
print("Number of rows and columns:", df.shape)
print("\nData types:\n", df.dtypes)
print("\nSummary statistics:\n", df.describe())
```

4.	Handling Missing Data:
*	The code checks for missing values in the dataset:
*	It uses the isnull().sum() method to calculate the sum of missing values in each column of the DataFrame.
*	It prints the count of missing values for each column.

```python
print("\nMissing values:\n", df.isnull().sum())
```

5.	Exploratory Data Analysis (EDA):
*	The code performs exploratory data analysis by creating example visualizations:
*	It creates a histogram of the 'Price' column using sns.histplot() and plt.show(), visualizing the distribution of prices.
*	It creates a boxplot to examine the relationship between the 'Rating' and 'Type' columns using sns.boxplot() and plt.show().

```python
plt.figure(figsize=(10, 6))
sns.histplot(df['Price'])
plt.title('Distribution of Price')
plt.show()

plt.figure(figsize=(10, 6))
sns.boxplot(x='Type', y='Rating', data=df)
plt.title('Rating by Dairy Product Type')
plt.show()
```

6.	Correlation Analysis:
*	The code calculates the correlation matrix of the dataset using df.corr().
*	It creates a heatmap visualization of the correlation matrix using sns.heatmap() and plt.show(). The heatmap provides a visual representation of the correlations between different numerical variables in the dataset.

```python
correlation_matrix = df.corr()
plt.figure(figsize=(10, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()
```

7.	Feature Engineering (if required):
*	The code demonstrates an example of feature engineering by creating a new feature called 'Price per Weight'. It calculates the price per weight by dividing the 'Price' column by the 'Weight' column.

```python
df['Price per Weight'] = df['Price'] / df['Weight']
```

8.	Additional Visualizations:
*	The code creates additional visualizations to explore relationships between variables:
*	It creates a scatter plot of 'Calories' versus 'Protein' with different colors representing different 'Type' categories using sns.scatterplot() and plt.show().

```python
plt.figure(figsize=(10, 6))
sns.scatterplot(x='Calories', y='Protein', data=df, hue='Type')
plt.title('Calories vs Protein by Dairy Product Type')
plt.show()
```


### Source code <br>

```python
# Importing Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Loading the Dataset
df = pd.read_csv('/content/dairy_products_dataset.csv')

# Understanding the Dataset
print("Number of rows and columns:", df.shape)
print("\nData types:\n", df.dtypes)
print("\nSummary statistics:\n", df.describe())

# Handling Missing Data
print("\nMissing values:\n", df.isnull().sum())

# Exploratory Data Analysis
# Example visualizations
plt.figure(figsize=(10, 6))
sns.histplot(df['Price'])
plt.title('Distribution of Price')
plt.show()

plt.figure(figsize=(10, 6))
sns.boxplot(x='Type', y='Rating', data=df)
plt.title('Rating by Dairy Product Type')
plt.show()

# Correlation Analysis
correlation_matrix = df.corr()
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()

# Feature Engineering (if required)
# Example: Creating a new feature 'Price per Weight'
df['Price per Weight'] = df['Price'] / df['Weight']

# Visualizations
plt.figure(figsize=(10, 6))
sns.scatterplot(x='Calories', y='Protein', data=df, hue='Type')
plt.title('Calories vs Protein by Dairy Product Type')
plt.show()
```


