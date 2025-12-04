# 📘 Advanced SQL on NULL Functions

## 📌 Summary of the Case Study
This case study demonstrates how **advanced SQL techniques** can be applied to handle **NULL values** in retail shopping trend data. The project focused on filtering missing values, replacing NULLs with defaults, classifying records using CASE statements, and performing aggregations with conditions. The goal was to transform incomplete raw data into **business insights** such as customer segmentation, purchase behavior, and review analysis.

---

## 🔍 How the Case Study Was Done
1. **Dataset Exploration**
   - Source: `MYDATABASE.PUBLIC.SHOPING_TREND_01`
   - Example columns:  
     `customer_id`, `size`, `purchase_amount`, `item_purchased`, `season`,  
     `payment_method`, `promo_code_used`, `review_rating`, `shipping_type`,  
     `location`, `color`, `previous_purchases`, `frequency_of_purchases`,  
     `category`, `age`, `gender`.

2. **SQL Query Development**
   - Designed **20 targeted queries** to address specific business questions:
     - Customers with missing size but purchase amount > 50.
     - Purchases grouped by season, replacing NULLs with "Unknown Season".
     - Payment method counts with NULLs treated as "Not Provided".
     - Classification of spenders (High, Medium, Low) using CASE + IFNULL.
     - Top 5 locations by purchase amount, replacing NULLs with 0.
     - Average review ratings per category, handling NULLs and filtering > 3.5.
     - Delivery speed classification using CASE logic.
     - Identification of customers with missing promo codes, shipping types, or review ratings.

3. **NULL Handling Techniques**
   - **IFNULL / COALESCE** → Replace missing values with defaults.  
   - **CASE WHEN** → Classify records and handle conditional logic.  
   - **Aggregations** → SUM, AVG, COUNT with conditions to exclude or include NULLs.  
   - **Filtering** → Queries designed to highlight missing or incomplete data.  

---

## 📊 Insights Found
- Customers with missing attributes (e.g., size, promo codes) still contributed significantly to sales.  
- Seasonal grouping revealed that **NULL seasons** represented a notable portion of transactions, requiring classification as "Unknown Season".  
- Payment method analysis showed gaps where customers did not provide details, highlighting areas for improved data capture.  
- **Spender classification** identified high-value customers even when purchase amounts were partially missing.  
- Location-based analysis revealed **top-performing regions**, while NULL handling ensured accurate revenue calculations.  
- Review ratings analysis showed that handling NULLs was critical to avoid skewed averages and to identify categories with strong customer satisfaction.  
- Delivery speed classification provided insights into customer preferences for shipping methods.  

---

## 🎯 Summary of Findings
By systematically handling NULL values, the project transformed incomplete retail data into **reliable insights**. The analysis uncovered:  
- Customer behavior patterns despite missing attributes.  
- Seasonal and regional sales trends.  
- Payment and promo code usage gaps.  
- Correlations between spending, reviews, and purchase frequency.  

This demonstrates how **advanced SQL functions** can improve data quality and deliver **business intelligence** that supports decision-making in **marketing, customer engagement, and inventory management**.

---

## 🛠️ Tools Used
- **SQL-compatible databases** (Snowflake, BigQuery, PostgreSQL, MySQL, SQL Server, Oracle)  
- **T-SQL / SQL functions** (IFNULL, COALESCE, CASE, SUM, AVG, COUNT, GROUP BY)  
- **Optional Visualization Tools**: Power BI, Excel (pivot tables, dashboards)  

