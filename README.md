📘 Advanced SQL on NULL Functions
📌 Overview
This project demonstrates advanced SQL techniques for handling NULL values in retail shopping trend data. The queries showcase:

Filtering missing values

Replacing NULLs with defaults using IFNULL

Classifying records with CASE

Aggregating and grouping with conditions

Business insights such as customer segmentation, purchase behavior, and review analysis

🛠️ Requirements
SQL-compatible database (Snowflake, BigQuery, PostgreSQL, MySQL, SQL Server, Oracle, etc.)

Dataset:

Code
MYDATABASE.PUBLIC.SHOPING_TREND_01
Example columns:

customer_id

size

purchase_amount

item_purchased

season

payment_method

promo_code_used

review_rating

shipping_type

location

color

previous_purchases

frequency_of_purchases

category

age

gender

📂 Queries
1. 🔎 Missing Size & Purchase > 50
sql
SELECT customer_id, size, purchase_amount, item_purchased
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE size IS NULL AND purchase_amount > 50;
2. 📅 Purchases by Season (NULL → Unknown)
sql
SELECT COUNT(*) AS total_purchases,
       IFNULL(season,'unknown season') AS season_new
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
GROUP BY IFNULL(season,'unknown season');
3. 💳 Customers by Payment Method (NULL → Not Provided)
sql
SELECT COUNT(*) AS customer_count,
       IFNULL(payment_method,'not provided') AS payment_method
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
GROUP BY payment_method;
4. 🎟️ Missing Promo Code & Low Rating
sql
SELECT customer_id, promo_code_used, review_rating, item_purchased
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE promo_code_used IS NULL AND review_rating < 3.0;
5. 🚚 Average Purchase by Shipping Type (NULL → 0)
sql
SELECT shipping_type,
       AVG(IFNULL(purchase_amount,0)) AS Average_purchase_amount
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
GROUP BY shipping_type;
6. 📍 Purchases per Location (>5, Non-NULL Payment)
sql
SELECT location, COUNT(*) AS total_purchases
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE payment_method IS NOT NULL
GROUP BY location
HAVING COUNT(*) > 5;
7. 💵 Spender Category (CASE + NULL Handling)
sql
SELECT customer_id,
       IFNULL(purchase_amount,0) AS purchase_amount,
       CASE
         WHEN IFNULL(purchase_amount,0) > 80 THEN 'High'
         WHEN IFNULL(purchase_amount,0) BETWEEN 50 AND 80 THEN 'Medium'
         ELSE 'Low'
       END AS spender_category
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01;
8. 🎨 Customers with Color Not NULL & Previous Purchases NULL
sql
SELECT customer_id, color, previous_purchases
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE color IS NOT NULL AND previous_purchases IS NULL;
9. 🔄 Group by Frequency of Purchases
sql
SELECT frequency_of_purchases, COUNT(*) AS total_purchase_amount
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
GROUP BY frequency_of_purchases;
10. 🛍️ Purchases per Category (Exclude NULL)
sql
SELECT category, COUNT(*) AS total_purchases
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE category IS NOT NULL
GROUP BY category;
11. 📍 Top 5 Locations by Purchase Amount
sql
SELECT location,
       SUM(IFNULL(purchase_amount,0)) AS Total_purchase_amount
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
GROUP BY location
ORDER BY Total_purchase_amount DESC
LIMIT 5;
12. 🚻 Entries with NULL Color by Gender & Size
sql
SELECT gender, size, COUNT(*) AS number_entries
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE color IS NULL
GROUP BY gender, size;
13. 📦 Items with >3 NULL Shipping Type
sql
SELECT item_purchased, COUNT(*) AS null_shipping_type_count
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE shipping_type IS NULL
GROUP BY item_purchased
HAVING COUNT(*) > 3;
14. 💳 Payment Method with NULL Review Rating
sql
SELECT payment_method, COUNT(*) AS missing_review_rating_count
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE review_rating IS NULL
GROUP BY payment_method;
15. ⭐ Average Review Rating per Category (>3.5)
sql
SELECT category,
       AVG(IFNULL(review_rating,0)) AS average_review_rating
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
GROUP BY category
HAVING AVG(IFNULL(review_rating,0)) > 3.5;
16. 🎨 Colors Missing in ≥2 Rows + Avg Age
sql
SELECT color, AVG(age) AS Average_age
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE color IS NULL
GROUP BY color
HAVING COUNT(*) >= 2;
17. 🚚 Delivery Speed Classification
sql
SELECT COUNT(*) AS customer_count,
       CASE
         WHEN shipping_type IN ('Express','Next Day Air') THEN 'Fast'
         WHEN shipping_type = 'Standard' THEN 'Slow'
         ELSE 'Other'
       END AS delivery_speed
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
GROUP BY delivery_speed;
18. 🎟️ Promo Code = Yes & Purchase Amount NULL
sql
SELECT customer_id, promo_code_used, purchase_amount
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE purchase_amount IS NULL AND promo_code_used = 'Yes';
19. 📍 Max Previous Purchases per Location (Avg Rating > 4.0)
sql
SELECT location,
       MAX(IFNULL(previous_purchases,0)) AS Max_previous_purchase,
       AVG(review_rating) AS average_review_rating
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
GROUP BY location
HAVING AVG(review_rating) > 4.0;
20. 🚚 NULL Shipping Type + Purchase Between 30–70
sql
SELECT customer_id, shipping_type, purchase_amount, item_purchased
FROM MYDATABASE.PUBLIC.SHOPING_TREND_01
WHERE shipping_type IS NULL AND purchase_amount BETWEEN 30 AND 70
