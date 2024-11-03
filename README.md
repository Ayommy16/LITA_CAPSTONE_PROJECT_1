# LITA_CAPSTONE_PROJECT_1

## Project Title: Sales Data Analysis

## Project Overview
This repository contains an analysis of sales data, including total sales by product, region, and month. Various metrics have been calculated to provide insights into sales performance


## Data Sources
The primary source of data used here is Sales Data.xslx downloaded from Canva LMS.

## Data Description
The dataset includes the following columns:

- **OrderID**: Unique identifier for each order.
- **Customer Id**: Unique identifier for customers.
- **Product**: Type of product sold (e.g., Gloves).
- **Region**: Geographic region where the sale occurred (e.g., South, West).
- **OrderDate**: Date of the order in MM/DD/YYYY format.
- **Quantity**: Number of items sold in the order.
- **UnitPrice**: Price per item sold.
- **Total Sales**: Total revenue generated from the order (calculated as Quantity x UnitPrice).

  ### Sample Data
| OrderID | Customer Id | Product | Region | OrderDate   | Quantity | UnitPrice | Total Sales |
|---------|-------------|---------|--------|-------------|----------|-----------|-------------|
| 1006    | Cus1141     | Gloves  | South  | 6/30/2023   | 8        | 25        | 200         |
| 1012    | Cus1234     | Gloves  | West   | 12/31/2023  | 5        | 20        | 100         |
| 1018    | Cus1288     | Gloves  | South  | 6/30/2024   | 12       | 25        | 300         |

## Tools Used
- Microsoft Excel for Data Cleaning and Visualization
- SQL- Structured Query Language for querying data to extract key insights based on some questions.
- PowerBI to visualize the insights found in Excel and SQL

 ## Excel Analysis Steps

### 1. Data Preparation
- The dataset is organized in a table format in Excel to facilitate analysis.
- All relevant data types (e.g., dates, numbers) are formatted appropriately.

### 2. Explorative Data Analysis 
This involved the exploration of Data to answer some questions on the Data such as:
- What is the overall total sales by products, region, and months
- What is the average sales per product and total revenue by region?

### 3. Creating Pivot Tables
Pivot tables were created to summarize sales data effectively. The following pivot tables were generated:

#### 3.1 Total Sales by Product
- **Steps**:
  - Insert a Pivot Table.
  - Drag `Product` to the Rows area.
  - Drag `Total Sales` to the Values area (set to SUM).
- **Output**: A summary table displaying total sales for each product.

#### 3.2 Total Sales by Region
- **Steps**:
  - Insert a new Pivot Table.
  - Drag `Region` to the Rows area.
  - Drag `Total Sales` to the Values area (set to SUM).
- **Output**: A summary table showing total sales by region.

#### 3.3 Total Sales by Month
- **Steps**:
  - Insert a new Pivot Table.
  - Drag `OrderDate` to the Rows area (group by Month).
  - Drag `Total Sales` to the Values area (set to SUM).
- **Output**: A summary table showing total sales for each month.

  #### 4.1 Average Sales per Product
  - **Steps**:
  - Insert a new Pivot Table.
  - Drag `Products` to the Rows area.
  - Drag `Total Sales` to the Values area (set to AVERAGE).
- **Output**: A summary table showing average sales per product.

### 4. Calculating Metrics
To derive additional insights, various metrics were calculated using Excel formulas.

## SQL Analysis

### Queries for Key Insights
Assuming you have a SQL table named `sales`, here are the SQL queries to extract insights:

#### 1. Total Sales for Each Product Category
```sql
SELECT Product, SUM(Total_Sales) AS Total_Sales
FROM sales
GROUP BY Product
```
This query retrieves total sales for each product, allowing you to identify top-selling items.

### 2. Number of Sales Transactions in Each Region
```sql
SELECT Region, COUNT(OrderID) AS Transaction_Count
FROM sales
GROUP BY Region;
```
- Purpose: This query counts the number of sales transactions per region, indicating regional activity levels.

### 3. Highest-Selling Product by Total Sales Value
```sql
SELECT Product, SUM(Total_Sales) AS Total_Sales
FROM sales
GROUP BY Product
ORDER BY Total_Sales DESC
LIMIT 1;
```
-Purpose: This query identifies the highest-selling product based on total sales value.

### 4. Total Revenue per Product
```sql
SELECT Product, SUM(Total_Sales) AS Total_Revenue
FROM sales
GROUP BY Product;
```
-Purpose: This query calculates total revenue for each product.

### 5.Monthly Sales Totals for the Current Year
```sql
SELECT DATE_FORMAT(OrderDate, '%Y-%m') AS Month, SUM(Total_Sales) AS Monthly_Sales
FROM sales
WHERE YEAR(OrderDate) = YEAR(CURDATE())
GROUP BY Month;
```
- Purpose: This query provides monthly sales totals for the current year, allowing for performance tracking over time.

### 6. Top 5 Customers by Total Purchase Amount
``` SELECT Customer_Id, SUM(Total_Sales) AS Total_Purchase
FROM sales
GROUP BY Customer_Id
ORDER BY Total_Purchase DESC
LIMIT 5;
```
-Purpose: This query identifies the top 5 customers based on their total purchase amounts.

### 7. Percentage of Total Sales Contributed by Each Region
```sql
SELECT Region, SUM(Total_Sales) AS Total_Sales,
       (SUM(Total_Sales) / (SELECT SUM(Total_Sales) FROM sales) * 100) AS Percentage_Contribution
FROM sales
GROUP BY Region;
```
-Purpose: This query calculates the percentage of total sales each region contributes.

### 8. Products with No Sales in the Last Quarter
```sql
SELECT Product
FROM sales
GROUP BY Product
HAVING SUM(CASE WHEN OrderDate >= DATE_SUB(CURDATE(), INTERVAL 3 MONTH) THEN Total_Sales ELSE 0 END) = 0;
```






