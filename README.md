# E_Commerce_Data_Analysis_Project Based on Python

This project focuses on analyzing e-commerce sales data to uncover insights into sales trends, customer behavior, and product performance. The analysis includes data cleaning, feature engineering, and visualizations to answer key business questions.

## Table of Contents
- [Project Description](#project-description)
- [Dataset Overview](#dataset-overview)
- [Data Cleaning and Preprocessing](#data-cleaning-and-preprocessing)
- [Analysis and Insights](#analysis-and-insights)
  - [Monthly Sales Analysis](#monthly-sales-analysis)
  - [Sales by Category](#sales-by-category)
  - [Sales by Sub-Category](#sales-by-sub-category)
  - [Monthly Profit Analysis](#monthly-profit-analysis)
  - [Profit by Category and Sub-Category](#profit-by-category-and-sub-category)
  - [Sales and Profit by Customer Segment](#sales-and-profit-by-customer-segment)
  - [Sales-to-Profit Ratio Analysis](#sales-to-profit-ratio-analysis)
- [Visualizations](#visualizations)
- [Conclusion](#conclusion)

## Project Description

This project aims to analyze e-commerce data to:

- Identify monthly sales and profit trends.
- Determine the best-performing product categories and sub-categories.
- Analyze customer segments based on sales and profitability.
- Evaluate the sales-to-profit ratio for better business decision-making.

The analysis is implemented using **Python** in a **Jupyter Notebook** environment.

## Dataset Overview

The dataset used in this project contains **9,994 rows** and **21 columns**.

### Key Columns:

| Column Name     | Description                                      |
|-----------------|--------------------------------------------------|
| Row ID          | Unique identifier for each row in the dataset.   |
| Order ID        | Unique identifier for each order.                |
| Order Date      | The date when the order was placed.              |
| Ship Date       | The date when the order was shipped.             |
| Ship Mode       | Shipping method used for the order.              |
| Customer ID     | Unique identifier for each customer.             |
| Customer Name   | Name of the customer.                            |
| Segment         | Customer segment (e.g., Consumer, Corporate).    |
| Country         | Country where the order was placed.              |
| City            | City where the order was placed.                 |
| State           | State where the order was placed.                |
| Postal Code     | Postal code of the delivery address.             |
| Region          | Region where the order was placed (e.g., East).  |
| Product ID      | Unique identifier for each product.              |
| Category        | Product category (e.g., Furniture, Technology).  |
| Sub-Category    | Sub-category of the product (e.g., Phones).      |
| Product Name    | Name of the product.                             |
| Sales           | Total sales amount for the order (in USD).       |
| Quantity        | Number of units sold in the order.               |
| Discount        | Discount applied to the order (as a percentage). |
| Profit          | Profit earned from the order (in USD).           |

### Dataset Characteristics:

- **Total Rows:** 9,994  
- **Total Columns:** 21  

### Data Types:

- **Object:** 15 columns (e.g., Customer Name, Category)  
- **Float64:** 3 columns (e.g., Sales, Profit)  
- **Int64:** 3 columns (e.g., Row ID, Quantity)

This dataset provides comprehensive information about e-commerce transactions and is ideal for analyzing sales, profit trends, customer behavior, and product performance.

## Data Cleaning and Preprocessing

Key steps in data preparation include:

- **Feature Extraction:**

  ```python
  data['Order Month'] = data['Order Date'].dt.month
  data['Order Year'] = data['Order Date'].dt.year
  data['Order Day of the week'] = data['Order Date'].dt.dayofweek
  ```

- **Handling Missing Values:** Ensured no missing values in critical columns like Sales and Profit.

- **Data Verification:** Displayed the first few rows to confirm changes:

  ```python
  data.head()
  ```

## Analysis and Insights

### Monthly Sales Analysis

**Objective:** Calculate total sales for each month and identify months with the highest and lowest sales.

```python
sales_by_month = data.groupby('Order Month')['Sales'].sum().reset_index()
```

**Insights:**
- **Highest Sales:** December had the highest sales.
- **Lowest Sales:** February had the lowest sales.

### Sales by Category

**Objective:** Analyze sales performance across different product categories.

```python
sales_by_category = data.groupby('Category')['Sales'].sum().reset_index()
```

**Insights:**
- **Top Category:** Technology has the highest sales.
- **Lowest Category:** Office Supplies has lower sales compared to other categories.

### Sales by Sub-Category

**Objective:** Analyze sales performance across different product sub-categories.

```python
sales_by_subcategory = data.groupby('Sub-Category')['Sales'].sum().reset_index()
```

**Insights:**
- **Top Sub-Category:** Phones have the highest sales.
- **Lowest Sub-Category:** Fasteners have the lowest sales.

| Sub-Category | Total Sales   |
|--------------|---------------|
| Phones       | 328,449.10    |
| Chairs       | 203,412.73    |
| Accessories  | 167,380.32    |
| Fasteners    | 3,024.28      |

### Monthly Profit Analysis

**Objective:** Analyze monthly profit trends to determine which month had the highest profit.

```python
profit_by_month = data.groupby('Order Month')['Profit'].sum().reset_index()
```

**Insights:**
- **Highest Profit Month:** March has the highest profit.
- **Lowest Profit Month:** January has the lowest profit.

| Month    | Total Profit   |
|----------|----------------|
| January  | 9,134.45       |
| February | 10,294.61      |
| March    | 28,594.69      |

### Profit by Category and Sub-Category

**Objective:** Analyze profitability across categories and sub-categories to identify key contributors.

```python
profit_by_category = data.groupby(['Category', 'Sub-Category'])['Profit'].sum().reset_index()
```

**Insights:**
- Technology is both highly profitable and generates significant revenue.
- Certain sub-categories like Fasteners have low profitability despite low sales.

### Sales and Profit by Customer Segment

**Objective:** Analyze customer segments based on their contribution to sales and profit.

```python
segment_analysis = data.groupby('Segment').agg({'Sales': 'sum', 'Profit': 'sum'}).reset_index()
```

**Insights:**
- The **Consumer** segment contributes most to overall sales.
- The **Corporate** segment shows a higher profit margin relative to its sales contribution.

### Sales-to-Profit Ratio Analysis

**Objective:** Evaluate how efficiently sales translate into profit for different categories or segments.

```python
data['Sales_to_Profit_Ratio'] = data['Profit'] / data['Sales']
ratio_analysis = data.groupby('Category')['Sales_to_Profit_Ratio'].mean().reset_index()
```

**Insights:**
- Categories with lower ratios may require cost optimization or pricing adjustments.

## Visualizations

- **Monthly Sales Trend:** A bar chart showing total sales for each month helps identify seasonal trends.

- **Sub-Category Sales Bar Chart:** A bar chart visualizing total sales by sub-category helps identify which products perform best.

- **Monthly Profit Line Chart:** A line chart showing monthly profit trends highlights seasonal profitability patterns.

- **Customer Segment Contribution Pie Chart:** A pie chart visualizing each segment's contribution to overall sales and profit.

**Example Code for Pie Chart:**

```python
import plotly.express as px

fig = px.pie(segment_analysis, names='Segment', values='Sales', title='Sales Contribution by Customer Segment')
fig.show()
```

## Conclusion

### Key Findings:

- **Phones** are the top-performing sub-category, while **Fasteners** show minimal sales.
- **March** is the most profitable month, indicating strong seasonal demand.
- **Technology** is both highly profitable and generates significant revenue.
- The **Consumer** segment contributes most to overall sales, while **Corporate** shows higher profitability margins.
- Categories with low **sales-to-profit** ratios may require strategic adjustments in pricing or cost management.

This project demonstrates how e-commerce businesses can leverage data analytics to drive decision-making, optimize inventory management, tailor marketing strategies, and improve financial performance.

