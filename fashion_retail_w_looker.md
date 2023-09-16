# Fashion Retail Analytics with Looker Studio
## Project Requirements Document: Business Performance Dashboard

**Author:** Mandy Wu (Business/Data/BI Analyst)
**Client/Sponsor:**

Alex Taylor (Retail Store Manager)
Emily Jones (Head of Sales)
Kai Smith (Product Manager)

**Purpose:**

The purpose of this project is to develop a dashboard to monitor key business operations, providing sponsors and stakeholders with valuable insights into critical business performance metrics. These insights will serve as the foundation for establishing key performance indicators (KPIs) for performance tracking and informed decision-making.

**Key Dependencies:**

* Team: Business/Data/BI Analyst (Mandy), Data Engineer (Julia)
* Primary Contacts: Alex Taylor, Emily Jones, Kai Smith
* Expected Deliverables: Dataset, dataset overview, dashboard development document, functional dashboard, set of KPIs
* Inter-Team Deliverables: User Acceptance Testing (UAT), bug reporting document

**Stakeholder Requirements:**

* **Primary Metrics:**
    * Total Sales Revenue: Understand the overall financial health by calculating total revenue generated from all orders.
    * Best-Selling Products: Optimize product offerings by identifying top-performing products and categories.
    * Customer Segmentation: Tailor marketing efforts and product recommendations by segmenting customers based on demographics and purchase behavior.
* **Secondary Metrics:**
    * Customer Lifetime Value (CLV): Assess long-term customer value for marketing and retention strategies.
    * Customer Retention Rate: Gain insights into customer satisfaction and loyalty by calculating the percentage of repeat customers.
    * Inventory Turnover Rate: Optimize stock levels by measuring inventory turnover.
    * Average Order Value (AOV): Plan pricing strategies and assess customer buying behavior by analyzing average order size.
    * Order Fulfillment Time: Ensure efficient order fulfillment and customer satisfaction by monitoring order processing times.
    * Gross Profit Margin: Assess product profitability and pricing strategies by calculating the gross profit margin.
    * Returns and Refunds Rate: Identify product quality issues and areas for improvement in customer service by tracking the percentage of orders resulting in returns or refunds.

**Prioritized Requirements:**

* R: Primary Metrics
* D: Secondary Metrics
* N: Accessibility

**Success Criteria:**

* **SMART Criteria:**
    * Specific: Clearly defined metrics and KPIs.
    * Measurable: Quantitative measurement of metrics.
    * Achievable: Realistic goals for improvements.
    * Relevant: Aligned with business objectives.
    * Time-bound: Defined timeframes for achieving improvements.

**User Journeys:**

* **Current User Experience:** Document existing user interactions with data and reports.
* **Future User Experience:** Define the enhanced user experience with the new dashboard.

**Assumptions:**

* The necessary datasets are available and accessible by the BI team.
* Stakeholder requirements have been accurately identified.
* The team possesses the required skills and resources to meet project deadlines.

**Compliance and Privacy:**

* Compliance with data privacy and security regulations will be ensured.
* Collaboration with the legal department to align data usage with company policies.

**Accessibility:**

* Keyboard navigation for mobility-impaired users.
* Alternative text for images and charts for users with visual impairments.
* High-contrast colors and clear fonts for users with low vision.
* Clear content structure with headings for improved comprehension.
* Use of plain language to enhance understanding.

**Data Visualization with Looker Studio:**

* The provided tables, including "Fashion retail product table," "Customers," "Orders," "OrderDetails," and "Payments," will be used as datasets for the dashboard.
* Looker Studio will be utilized to create interactive data visualizations and dashboards based on the defined metrics and KPIs.
* Visualizations will include bar charts, line charts, pie charts, and other relevant chart types to represent the metrics effectively.
* The Looker Studio environment will allow for data exploration, interactive filtering, and drill-down functionality.
* Scheduled deliveries of dashboard reports will be configured to relevant stakeholders for ongoing monitoring.

----------------------------------------------------------------------------------------------------------------

## The Dataset

![Tables and Schema](https://github.com/wusinyee/SYW-Portfolio-v2023/blob/391580c0e5993b46c4f87fc4b51e50cd39bb1eaa/dbtable.jpg)

### 1. Understanding the Dataset

### Summary Statistics for Fashion Retail Product Table

| Metric          | Value        |
|-----------------|--------------|
| count           | 1000.000000  |
| mean            | 1477.876000  |
| std             | 587.919142   |
| min             | 500.000000   |
| 25%             | 959.500000   |
| 50%             | 1460.500000  |
| 75%             | 2007.500000  |
| max             | 2500.000000  |






### Summary Statistics for Customers Table

| Column | Count | Unique | Top | Freq |
|---|---|---|---|---|
| customer_id | 1000 | 1000 | 7bSt5903 | 1 |
| first_name | 1000 | 938 | Grier | 3 |
| last_name | 1000 | 983 | Grooby | 3 |
| email | 970 | 970 | aarnaud0@baidu.com | 1 |
| gender | 1000 | 2 | Female | 508 |

|         address         | count |
|------------------------|-------|
| count                  | 984   |
| unique                 | 984   |
| top     1149 Nevada Center | 1     |
| freq                   |       |


### Summary Statistics for Orders Table

|     order_id      |    Value     |
|-------------------|--------------|
| count             | 1000.000000  |
| mean              | 50845.098000 |
| std               | 29106.505716 |
| min               | 47.000000    |
| 25%               | 25420.250000 |
| 50%               | 50684.000000 |
| 75%               | 76199.000000 |
| max               | 99972.000000 |


### Summary Statistics for Order Details Table

|   orderdetail_id   |   order_id   |   quantity   |
|-------------------|--------------|--------------|
| count             | 1000.000000  | 1000.000000  |
| mean              | 492303.898000 | 51234.825000 |
| std               | 287495.418152 | 28461.800343 |
| min               | 102.000000   | 50.000000    |
| 25%               | 262044.000000 | 26655.750000 |
| 50%               | 483870.000000 | 51137.000000 |
| 75%               | 744491.250000 | 76377.500000 |
| max               | 999301.000000 | 99962.000000 |


### Summary Statistics for Payments Table:
|   order_id   |    Value     |
|-------------|--------------|
| count       | 1000.000000  |
| mean        | 51040.741000 |
| std         | 28183.893463 |
| min         | 182.000000   |
| 25%         | 26701.500000 |
| 50%         | 52241.000000 |
| 75%         | 74875.000000 |
| max         | 99902.000000 |


## Data Types for Fashion Retail Product Table

| Column | Data Type |
|---|---|
| product_id | object |
| product_name | object |
| product_category | object |
| description | object |
| price | object |
| stock_quantity | int64 |

## Null Values for Fashion Retail Product Table

| Column | Null Values |
|---|---|
| product_id | 0 |
| product_name | 0 |
| product_category | 0 |
| description | 0 |
| price | 0 |
| stock_quantity | 0 |


