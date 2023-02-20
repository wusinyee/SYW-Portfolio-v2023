<h1 align="center">MySQL Data Cleaning Demonstration</h1>
The following procedures import "marketing_campaign.csv" (Kaggle, 2023) into a MySQL database and create a corresponding table:

```sql
CREATE DATABASE IF NOT EXISTS mydatabase;   -- create database if not exists

USE mydatabase;   -- use the database

CREATE TABLE IF NOT EXISTS marketing_campaign (
  id INT PRIMARY KEY,
  profession VARCHAR(100),
  marital VARCHAR(100),
  education VARCHAR(100),
  default_credit VARCHAR(100),
  balance INT,
  housing VARCHAR(100),
  loan VARCHAR(100),
  contact VARCHAR(100),
  day INT,
  month VARCHAR(100),
  duration INT,
  campaign INT,
  pdays INT,
  previous INT,
  poutcome VARCHAR(100),
  y VARCHAR(100)
);   -- create table

LOAD DATA INFILE 'C:/Users/syw10/OneDrive/桌面/Data Analytics Portfolio/Portfolio/Customer Personality Analysis/archive/marketing_campaign.csv'
INTO TABLE marketing_campaign
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;   -- import data from CSV file into table
```

The SQL script cleans the data in 'marketing_campaign' table as follows:

```sql
USE mydatabase;   -- use the database

-- Remove duplicates
DELETE FROM marketing_campaign 
WHERE id IN (
    SELECT id FROM (
        SELECT id, ROW_NUMBER() OVER(PARTITION BY profession, marital, education, default_credit, balance, housing, loan, contact, day, month, duration, campaign, pdays, previous, poutcome, y ORDER BY id) AS rn
        FROM marketing_campaign
    ) AS t
    WHERE t.rn > 1
);

-- Replace missing values in the `balance` column with the average balance
UPDATE marketing_campaign
SET balance = (SELECT AVG(balance) FROM marketing_campaign WHERE balance IS NOT NULL)
WHERE balance IS NULL;

-- Replace missing values in the `default_credit` column with 'unknown'
UPDATE marketing_campaign
SET default_credit = 'unknown'
WHERE default_credit IS NULL;

-- Remove outliers in the `duration` column
DELETE FROM marketing_campaign
WHERE duration > 1000;

-- Create a new column for the month as a number
ALTER TABLE marketing_campaign
ADD COLUMN month_num INT;

UPDATE marketing_campaign
SET month_num = CASE 
    WHEN month = 'jan' THEN 1
    WHEN month = 'feb' THEN 2
    WHEN month = 'mar' THEN 3
    WHEN month = 'apr' THEN 4
    WHEN month = 'may' THEN 5
    WHEN month = 'jun' THEN 6
    WHEN month = 'jul' THEN 7
    WHEN month = 'aug' THEN 8
    WHEN month = 'sep' THEN 9
    WHEN month = 'oct' THEN 10
    WHEN month = 'nov' THEN 11
    WHEN month = 'dec' THEN 12
END;

-- Remove the original `month` column
ALTER TABLE marketing_campaign
DROP COLUMN month;

-- Update the `poutcome` column to replace 'nonexistent' with 'unknown'
UPDATE marketing_campaign
SET poutcome = 'unknown'
WHERE poutcome = 'nonexistent';
```
This script includes several common data cleaning operations, such as removing duplicates, filling in missing values, removing outliers, and transforming data into a more usable format.
