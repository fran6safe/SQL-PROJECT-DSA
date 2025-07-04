# SQL-PROJECT-DSA
# 📊 KMS Sales Intelligence with SQL Server (2009–2012)

## ✨ Project Overview

This project was completed as part of the **Digital SkillUp Africa (DSA)** Data Analytics training. The analysis focuses on historical sales data from **Kultra Mega Stores (KMS)** — a retail and corporate office supply chain based in Lagos, Nigeria — with operations across various regions from **2009 to 2012**.

KMS management tasked us with deriving **actionable insights** to improve business performance using **structured data analysis** and **SQL queries**. The goal was to understand:

- How different regions, customer segments, and products performed
- Where the company is losing money through shipping or underperforming customers
- What decisions can improve profitability and customer retention

As the **Data Analyst**, I led the end-to-end process:
- Data ingestion using SQL Server Management Studio
- Data cleaning, transformation, and type optimization
- Formulation of real business questions
- Writing SQL queries to extract insights
- Summarizing recommendations to support strategic decision-making

🛠 **Tools Used:**
- SQL Server Management Studio (SSMS)
- Flat File Import Wizard
- Microsoft Excel (for initial data prep)
- GitHub (for version control and documentation)

📈 **Business Outcomes:**
- Identified top- and bottom-performing customer segments and products
- Diagnosed costly shipping patterns and misaligned logistics
- Proposed recommendations for marketing, logistics, and operations teams

---

## 📥 Data Importation Process

- **Source:** CSV file containing order data from 2009–2012.
- **Tool:** SQL Server Management Studio (SSMS) Flat File Import Wizard.
- **Steps:**
  1. Imported the dataset using the SSMS Flat File Import Wizard.
  2. Changed column data types to optimize performance and ensure data consistency:
     - `Sales`, `Profit`, `Discount`, `Shipping_Cost` → `DECIMAL(10,2)`
     - `Quantity`, `Order_ID`, `Product Count` → `INT`
  3. Cleaned column names and removed blank rows.
  4. Verified the import success through sampling and quick queries.

📸 *Screenshots of the import process and outputs are available in the `/images` folder.*

---

## 🔍 Business Questions & SQL Solutions

### 1️⃣ Which product category had the highest number of entries?

```sql
SELECT TOP 1 Product_Category, COUNT(Product_Category) AS [Product Count]
FROM KMS
GROUP BY Product_Category
ORDER BY [Product Count] DESC;
```

---

### 2️⃣ What are the top 3 and bottom 3 regions in terms of sales?

```sql
-- Top 3 regions
SELECT TOP 3 Region, SUM(Sales) AS [Total Sales]
FROM KMS
GROUP BY Region
ORDER BY [Total Sales] DESC;

-- Bottom 3 regions
SELECT TOP 3 Region, SUM(Sales) AS [Total Sales]
FROM KMS
GROUP BY Region
ORDER BY [Total Sales] ASC;
```

---

### 3️⃣ What were the total sales of applicants in Ontario?

```sql
SELECT Region, SUM(Sales) AS [Total Sales]
FROM KMS
WHERE Region = 'Ontario'
GROUP BY Region;
```

---

### 4️⃣ Advice the management of KMS on what to do to increase the revenue from the bottom 10 customers.

```sql
SELECT TOP 10 Customer_Name, SUM(Sales) AS [Total Sales]
FROM KMS
GROUP BY Customer_Name
ORDER BY [Total Sales] ASC;
```

💡 **Recommendations:**
- Create tailored promotions and discounts for inactive customers.
- Reach out directly to low-performing customers to understand why they stopped buying.
- Offer loyalty programs and exclusive deals.
- Provide better after-sales support.
- Run surveys to collect feedback and adjust strategy accordingly.

---

### 5️⃣ KMS incurred the most shipping cost using which shipping method?

```sql
SELECT TOP 1 Ship_Mode, SUM(Shipping_Cost) AS [Total Shipping Cost]
FROM KMS
GROUP BY Ship_Mode
ORDER BY [Total Shipping Cost] DESC;
```

---

### 6️⃣ Who are the most valuable customers, and what products or services did they typically purchase?

```sql
SELECT Customer_Name, Product_Name, SUM(Sales) AS [Total Sales]
FROM KMS
GROUP BY Customer_Name, Product_Name
ORDER BY [Total Sales] DESC;
```

---

### 7️⃣ Which small business customer had the highest sales?

```sql
SELECT TOP 1 Customer_Name, Customer_Segment, SUM(Sales) AS [Total Sales]
FROM KMS
WHERE Customer_Segment = 'Small Business'
GROUP BY Customer_Name, Customer_Segment
ORDER BY [Total Sales] DESC;
```

---

### 8️⃣ Which corporate customer placed the most number of orders from 2009 to 2012?

```sql
SELECT TOP 1 Customer_Name, Customer_Segment, COUNT(Order_ID) AS [Total Orders]
FROM KMS
WHERE Customer_Segment = 'Corporate' AND Order_Date BETWEEN '2009' AND '2012'
GROUP BY Customer_Name, Customer_Segment
ORDER BY [Total Orders] DESC;
```

---

### 9️⃣ Which consumer customer was the most profitable one?

```sql
SELECT TOP 1 Customer_Name, Customer_Segment, SUM(Profit) AS [Total Profit]
FROM KMS
WHERE Customer_Segment = 'Consumer'
GROUP BY Customer_Name, Customer_Segment
ORDER BY [Total Profit] DESC;
```

---

### 🔟 Which customers returned items, and what segments do they belong to?

```sql
SELECT Customer_Name, Customer_Segment, Status
FROM KMS
JOIN dbo.Order_Status ON KMS.Order_ID = Order_Status.Order_ID;
```

---

### 1️⃣1️⃣ If the delivery truck is the most economical but the slowest shipping method and express air is the fastest but most expensive one, did you think the company appropriately spent shipping costs based on the order priority?

```sql
SELECT Order_Priority, Ship_Mode,
       COUNT(Order_ID) AS [Order Count],
       SUM(Sales - Profit) AS [Estimated Shipping Cost],
       AVG(DATEDIFF(DAY, Order_Date, Ship_Date)) AS [Avg Ship Date]
FROM KMS
GROUP BY Order_Priority, Ship_Mode
ORDER BY Order_Priority, Ship_Mode DESC;
```

🧠 **Insight:**  
No, KMS did **not** appropriately align shipping cost with priority.  
- Express Air (best for high-priority orders) was underused.  
- Delivery Truck (slower, cheaper) was overused even for urgent orders.  
- This mismatch results in **wasted cost and delayed deliveries**.

---

## 📈 Summary of Findings

- **Most Sold Category:** Office Supplies  
- **Top Region by Sales:** West  
- **Least Performing Region:** Nunavut or Territories  
- **Most Profitable Segment:** Consumer  
- **Most Costly Shipping Mode:** Express Air  
- **Major Insight:** Misalignment between order priority and shipping method caused unnecessary costs.

---

## 📁 Repository Structure

```
kms-sql-analysis/
├── README.md
├── data/
│   └── kms_orders.csv
├── scripts/
│   └── kms_analysis.sql
├── images/
│   ├── flat-file-import.png
│   ├── region-sales-chart.png
│   ├── customer-segmentation.png
│   └── shipping-analysis.png
```

---

## 🧠 Skills Demonstrated

- SQL Server T-SQL Querying  
- Flat File Data Import & Cleaning  
- Data Type Conversion & Optimization  
- Real-world BI Question Solving  
- Shipping Strategy Evaluation  
- Customer Value & Profitability Analysis  

---
[sql](https://drive.google.com/open?id=10r3eP8YzNziwFMEycwUH-1rqYQTsS5Qx&usp=drive_fs)
## 🔗 Connect With Me

👤 **Oladipupo Abidemi Francis**  
🔗 [LinkedIn](www.linkedin.com/in/fran7safe)

---

## 🚀 Future Enhancements

- Build dynamic dashboards using **Power BI**  
- Automate queries into **stored procedures**  
- Use **Python or Power Query** for predictive analytics  
- Integrate CRM insights for sales forecasting  
