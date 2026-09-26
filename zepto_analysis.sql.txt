DROP TABLE IF EXISTS zepto;

CREATE TABLE zepto (
    sku_id INT AUTO_INCREMENT PRIMARY KEY,
    category VARCHAR(120),
    name VARCHAR(150) NOT NULL,
    mrp DECIMAL(8,2),
    discountPercent DECIMAL(5,2),
    availableQuantity INT,
    discountedSellingPrice DECIMAL(8,2),
    weightInGms INT,
    outOfStock VARCHAR(10),
    quantity INT
);

SELECT *  FROM zepto;

-- Null values
SELECT * FROM zepto WHERE name IS NULL
OR 
category IS NULL
OR
mrp IS NULL
OR
discountPercent IS NULL
OR
weightInGms IS NULL
OR
availableQuantity IS NULL
OR
outOfStock IS NULL
OR
quantity IS NULL;

-- Different product Categories
SELECT DISTINCT category
FROM zepto
ORDER BY category;

-- Products out of stock vs in stock
SELECT outOfStock, COUNT(sku_id)
FROM zepto
GROUP BY outOfStock;

-- Product names present multiple times
SELECT name, COUNT(sku_id) as "Number of SKUs"
FROM zepto
GROUP BY name
HAVING count(sku_id)>1
ORDER BY count(sku_id) DESC;

-- Data Cleaning

-- Products with price 0
SELECT * FROM zepto
WHERE mrp=0 OR discountedSellingPrice=0;

SET SQL_SAFE_UPDATES = 0;
DELETE FROM zepto
WHERE mrp=0;

-- Convert paise to rupees
UPDATE zepto
SET mrp=mrp/100.0,
discountedSellingPrice = discountedSellingPrice/100.0;

SELECT * FROM zepto;

-- Q1. Find top 10 best-value products based on the discounted percentage
SELECT DISTINCT name, mrp, discountPercent
FROM zepto
ORDER BY discountPercent DESC
LIMIT 10;

-- Q2. Products with high price and out of stock
SELECT DISTINCT name, mrp
FROM zepto
WHERE outOfStock='TRUE' and mrp>300
ORDER BY mrp DESC;

-- Q3. Calculate estimated revenue for each category
SELECT category,
SUM(discountedSellingPrice * availableQuantity) AS total_revenue
FROM zepto
GROUP BY category
ORDER BY total_revenue;

-- Q4. products where mrp>500 and discount<10%
SELECT DISTINCT name, mrp, discountPercent
FROM zepto
WHERE mrp> 500 AND discountPercent<10
ORDER BY mrp DESC, discountPercent DESC;

-- Q5. Top 5 categories offering highest average
SELECT category, 
ROUND(AVG(discountPercent),2) AS avg_discount
FROM zepto
GROUP BY category
ORDER BY avg_discount DESC
LIMIT 5;

-- Q6. Find the price per gram for products above 100g and sort by best value
SELECT DISTINCT name, weightInGms, discountedSellingPrice,
ROUND(discountedSellingPrice/weightInGms,2) AS price_per_gram
FROM zepto
WHERE weightInGms >=100
ORDER BY price_per_gram;

-- Q7. Group the products into categories like low, med, bulk
SELECT DISTINCT name, weightInGms,
CASE WHEN weightInGms < 1000 THEN 'Low'
	WHEN weightInGms < 5000 THEN 'Medium'
    ELSE 'Bulk'
    END AS weight_category
FROM zepto;

-- Q8. Total inventory weight per category
SELECT category,
SUM(weightInGms * availableQuantity) AS total_weight
FROM zepto
GROUP BY category
ORDER BY total_weight DESC;

    



