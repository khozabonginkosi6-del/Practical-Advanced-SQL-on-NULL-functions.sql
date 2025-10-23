---Practical Advanced SQL on NULL Functions----

SELECT*
FROM
"MYDATABASE"."PUBLIC"."SHOPING_TREND_01";

-------#1:find all records where siz is missing and the purchase_amount is greater than 50--------
SELECT
  customer_id,
  size,
  purchase_amount,
  item_purchased
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
WHERE size IS NULL
AND purchase_amount > 50;

--------#2:List the total number of purchases grouped by Season, treating NULL values as 'Unknown Season'-----------
SELECT
count(*) AS total_purchases,
IFNULL(season,'unknown season') As season_new
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  GROUP BY IFNULL(season,'unknown season');
  
-----#3:Count how many customers used each Payment Method, treating NULLs as 'Not Provided'.------
 SELECT
count(*) AS customer_count,
IFNULL(payment_method,'not provided') As payment_method
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  GROUP BY ALL;

----#4:Show customers where Promo Code Used is NULL and Review Rating is below 3.0---- 

SELECT
customer_id,
promo_code_used,
review_rating,
item_purchased
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
where promo_code_used IS NULL 
AND review_rating < 3.0;

---#5:Group customers by Shipping Type, and return the average purchase_amount, treating missing values as 0----

SELECT
shipping_type,
AVG(IFNULL(purchase_amount,0)) AS Average_purchase_amount
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
GROUP BY shipping_type;
  
---#6:Display the number of purchases per Location only for those with more than 5 purchases and no NULL Payment Method--- 

SELECT
location,
count(*) As total_purchases
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
where payment_method is not null
group by location
having count(*) >5;

---#7:Create a column Spender Category that classifies customers using CASE----
---'High' if amount > 80, 'Medium' if BETWEEN 50 AND 80
---'Low' otherwise
---Replace NULLs in purchase_amount with 0
---Customer ID, purchase_amount, Spender Category
 SELECT
    customer_id,
    IFNULL(purchase_amount, 0) AS purchase_amount,
    CASE
        WHEN IFNULL(purchase_amount, 0) > 80 THEN 'High'
        WHEN IFNULL(purchase_amount, 0) BETWEEN 50 AND 80 THEN 'Medium'
        ELSE 'Low'
    END AS spender_category
FROM
    "MYDATABASE"."PUBLIC"."SHOPING_TREND_01";
    

    ---#8:Find customers who have no Previous Purchases value but whose Color is not NULL---
SELECT
customer_id,
color,
previous_purchases
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
 WHERE color IS NOT NULL
 AND previous_purchases IS NULL;

 ---#9:Group records by Frequency of Purchases and show the total amount spent per group, treating NULL frequencies as 'Unknown'---
 SELECT
 frequency_of_purchases,
 count(*) As total_purchase_amount
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  GROUP BY frequency_of_purchases;

---#10:Display a list of all Category values with the number of times each was purchased, excluding rows where Categoryis NULL---
 SELECT
 category,
 count(*) As total_purchases,
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  WHERE category IS NULL
  GROUP BY category;

  ---#11:Return the top 5 Locations with the highest total purchase_amount, replacing NULLs in amount with 0---
SELECT
 location,
 SUM(IFNULL(purchase_amount,0)) As Total_purchase_amount
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  GROUP BY
    location
  ORDER BY
      total_purchase_amount
  DESC LIMIT 5;

  ---#12:Group customers by Gender and Size, and count how many entries have a NULL Color---
   SELECT
   gender,
   size,
   count(*) as number_entries
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  WHERE color is NULL
  GROUP BY
    gender,
    size;

---#13:Identify all Item Purchased where more than 3 purchases had NULL Shipping Type---
 SELECT
   item_purchased,
   count(*) as null_shipping_type_count
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  WHERE shipping_type is NULL
  GROUP BY
   item_purchased
   HAVING COUNT(*) > 3;

---#14:Show a count of how many customers per Payment Method have NULL Review Rating---
 SELECT
   payment_method,
   count(*) as missing_review_rating_count
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  WHERE review_rating is NULL
  GROUP BY
   payment_method;

 ---#15:Group by Category and return the average Review Rating, replacing NULLs with 0, and filter only where average is greater than 3.5---

    SELECT
   category,
   AVG(IFNULL(review_rating,0)) As average_review_rating
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
  GROUP BY
   category
   HAVING AVG(IFNULL(review_rating,0)) > 3.5;

----#16:List all Colors that are missing (NULL) in at least 2 rows and the average Age of customers for those rows----

SELECT
    color,
    AVG(age) As Average_age
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
WHERE color IS NULL
GROUP BY
   color
 HAVING COUNT(*) >= 2;

 ---#17:Use CASE to create a column Delivery Speed: 'Fast' if Shipping Type is 'Express' or----
 ---'Next Day Air', 'Slow' if 'Standard',
 ---'Other' for all else including NULL. Then count how many customers fall into
 ----each category
 SELECT
    count(*) As customer_count,
    CASE
    WHEN shipping_type IN ('Express','Next Day Air') THEN 'fast'
    WHEN shipping_type = 'standard' THEN 'Slow'
    ELSE 'Other'
    END AS delivery_speed
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
GROUP BY
 delivery_speed;

 
 ----#18:Find customers whose purchase_amount is NULL and whose Promo Code Used is 'Yes'--- 
 SELECT
  customer_id,
  promo_code_used,
  purchase_amount
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
WHERE purchase_amount IS NULL
AND promo_code_used = 'yes';

---#19:Group by Location and show the maximum Previous Purchases, replacing NULLs with 0, only where the average rating is above 4.0---
 SELECT
  location,
  MAX(IFNULL(previous_purchases,0)) AS Max_previous_purchase,
  AVG(review_rating) as avarege_review_rating
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
GROUP BY location
HAVING AVG(review_rating) > 4.0;

---#20:Show customers who have a NULL Shipping Type but made a purchase in the range of 30 to 70 USD---
SELECT
  customer_id,
  shipping_type,
  purchase_amount,
  item_purchased
FROM
  "MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
WHERE shipping_type IS NULL
AND purchase_amount BETWEEN 30 AND 70;


SELECT*
FROM
"MYDATABASE"."PUBLIC"."SHOPING_TREND_01"
