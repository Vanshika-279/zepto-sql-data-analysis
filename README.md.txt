# Zepto SQL Data Analysis

## 📌 Project Overview

This project analyzes a Zepto product dataset using SQL and MySQL.

The objective is to explore product information, identify duplicate products, analyze pricing and discounts, and examine product availability using SQL queries.

## 🛠️ Tech Stack

- MySQL
- SQL
- MySQL Workbench

## 📂 Dataset

The dataset contains information about Zepto products, including:

- Product category
- Product name
- MRP
- Discount percentage
- Available quantity
- Discounted selling price
- Product weight
- Stock availability
- Quantity

## 🗃️ Database Structure

The main table used in this project is `zepto`.

| Column | Description |
|---|---|
| `sku_id` | Unique product identifier |
| `category` | Product category |
| `name` | Product name |
| `mrp` | Maximum retail price |
| `discountPercent` | Discount percentage |
| `availableQuantity` | Available quantity |
| `discountedSellingPrice` | Selling price after discount |
| `weightInGms` | Product weight in grams |
| `outOfStock` | Stock availability |
| `quantity` | Product quantity |

## 🔍 Analysis Performed

The project covers:

- Data cleaning
- Filtering using `WHERE`
- Aggregate functions
- `COUNT()`
- `AVG()`
- `GROUP BY`
- `HAVING`
- `ORDER BY`
- `DISTINCT`
- Duplicate detection
- Product pricing analysis
- Stock availability analysis

## 📊 Example Queries

### Duplicate Product Names

```sql
SELECT
    name,
    COUNT(sku_id) AS "Number of SKUs"
FROM zepto
GROUP BY name
HAVING COUNT(sku_id) > 1
ORDER BY COUNT(sku_id) DESC;

🎯 Learning Outcomes

Through this project, I practiced:

Working with a real-world dataset
Creating and managing MySQL tables
Cleaning data using SQL
Grouping and aggregating data
Identifying duplicate records
Filtering and sorting analytical results
Analyzing product pricing and availability

📁 Project Structure

zepto-sql-data-analysis/
│
├── zepto_analysis.sql
├── zepto_v2.csv
└── README.md

🚀 How to Run

1. Install MySQL and MySQL Workbench.
2. Clone this repository.
3. Open zepto_analysis.sql in MySQL Workbench.
4. Create the database and table.
5. Import zepto_v2.csv into the zepto table.
6. Execute the analysis queries.

👩‍💻 Author

Vanshika Chiratanagalla

