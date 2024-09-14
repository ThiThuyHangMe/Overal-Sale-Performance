# Flashsale Executive Summary - Shopee Vietnam

## 🎯 1. Summary

**Project Name**: Flashsale Executive Summary - Shopee Vietnam  
**Tools**: Excel, SQL, Tableau  

The June 2022 FlashSale Dashboard provides a comprehensive overview of flash sale performance, helping decision-makers evaluate its effectiveness. Key performance indicators such as order count, GMV (in USD), and stock sold offer valuable insights for planning future flash sales.

### Key Metrics:
- **Orders**: Displays total orders in June 2022, providing a snapshot of customer engagement.
- **GMV (USD)**: Represents the total sales value, directly assessing revenue impact.
- **Stock Sold**: Tracks the number of products sold, revealing demand trends crucial for inventory planning.

This dashboard centralizes essential performance metrics, saving time and resources while providing predictive analytics and recommendations that empower managers and team leaders to optimize future flash sales.

In conclusion, the June 2022 FlashSale Dashboard offers critical insights to evaluate flash sale performance and guide strategic actions for future success. Its user-friendly design, predictive analytics, and actionable recommendations make it an invaluable tool for optimizing flash sale strategies.

---

## 🔎 2. Grasp the Information

### Data File Summary:
- **Size**: 42.6 MB  
- **Rows**: 63,478  
- **Columns**: 41  

---

## ⚙️ 3. Preparing and Presenting Data

### Step 1: Clean the Data
- Eliminate NULL values
- Standardize formatting in date columns
- Discard unnecessary columns

### Step 2: Generate the Target Data Using SQL

#### SQL Queries:
* **Product Name Cleaning**:
   ```sql
   CASE 
       WHEN item_name NOT LIKE '%]%' THEN item_name 
       WHEN item_name LIKE '%]%' THEN SUBSTRING(item_name, CHARINDEX(']', item_name) + 2, LEN(CONVERT(nvarchar(max), item_name))) 
   END AS item_name
* **SQL Query for discount price label**:
   ```sql
   , CONCAT(CAST((fs_price / price_before_discount) * 100 AS DECIMAL(5, 2)), '%') AS discount_rate
    ,       CASE 
                WHEN (CAST((fs_price / price_before_discount) * 100 AS DECIMAL(5, 2))) > 70 THEN 'High Discount'
                WHEN (CAST((fs_price / price_before_discount) * 100 AS DECIMAL(5, 2))) <10 THEN 'Low Discount'
                ELSE 'Normal Discount'
            END AS discount_level
* **SQL Query for rebate label**
  ```sql
        , CASE 
            WHEN fs_rebate > 500000 THEN 'High Rebate'
            WHEN fs_rebate = 0 THEN 'Non Rebate'
            ELSE 'Low Rebate'
         END AS discount_level

* **SQL Query to filter Sellers Excluding CB Shop and Mall Shop**
  ```sql
   WHERE is_cb_shop = 0 and is_mall_shop = 0
