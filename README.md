# Project
# 🛒 Retail Business Performance & Profitability Analysis

## 📌 Overview
This project explores a transactional retail dataset to:
- Uncover loss-generating product categories  
- Assess inventory efficiency  
- Identify seasonal sales trends  
- Provide actionable strategies for business optimization  

## 🧰 Tools Used
- **SQL** – Profitability calculations by category  
- **Python (Pandas, Seaborn)** – EDA, correlation & inventory analysis  
- **Tableau** – Interactive dashboard for key business insights  

## 📂 Dataset
- File: `retail_store_inventory.csv`  
- Fields: Product ID, Category, Region, Date, Units Sold, Inventory Level, Price, Discount, Competitor Pricing, etc.

---

## 📊 Project Structure

### 1. 📁 Data Preparation (Python)
- Loaded and cleaned data using `pandas`
- Renamed columns for SQL compatibility
- Checked for missing/duplicate values

### 2. 📈 Exploratory Data Analysis (EDA)
- Visualized distributions (histograms, bar plots, heatmaps)
- Region & category analysis
- Seasonal sales trends
- Weak correlation between Inventory Days & Profitability

### 3. 🧮 SQL Profitability Analysis
Calculated:
- Total Revenue  
- Adjusted Total Profit  
- Profit Margin %

```sql
SELECT Category,
       ROUND(SUM(Price * Units_Sold), 2) AS Total_Revenue,
       ROUND(SUM((Price - Competitor_Pricing) * (1 - Discount/100.0) * Units_Sold), 2) AS Total_Profit,
       ROUND((SUM((Price - Competitor_Pricing) * (1 - Discount/100.0) * Units_Sold) * 100.0) /
             NULLIF(SUM(Price * Units_Sold), 0), 2) AS Profit_Margin_Percent
FROM retail
GROUP BY Category
ORDER BY Profit_Margin_Percent ASC;
```

### 4. 📦 Inventory & Profitability (Python)
- Calculated `Profit_per_unit`, `Total_Profit`, and `Inventory_Days`
- Identified:
  - **Slow Movers** (High Inventory Days, Negative Profit)
  - **Overstocked Items** (Low sales, high inventory)

```python
df['Profit_per_unit'] = (df['Price'] - df['Competitor_Pricing']) * (1 - df['Discount'] / 100)
df['Total_Profit'] = df['Units_Sold'] * df['Profit_per_unit']
df['Inventory_Days'] = df['Inventory_Level'] / df['Units_Sold'].replace(0, 1)
```

- Correlation (Inventory Days vs Total Profit): **r = 0.001**

### 5. 📊 Tableau Dashboard
Interactive views for:
- Profitability by Region & Category  
- Seasonal sales performance  
- Inventory vs Profit scatter plot  
- Overstocked product IDs  

---

## 💡 Key Insights
- ✅ **Toys**: Only profitable category  
- ❌ **Clothing**: Most loss-making  
- 📉 **North**: Worst-performing region  
- 📦 Overstocked SKUs: High inventory, low demand  
- ❄️ **Winter**: Lowest seasonal sales  

---

## 🎯 Recommendations
- 🔥 Run clearance campaigns for slow movers  
- 💰 Adjust pricing strategy in Groceries & Clothing  
- 📦 Optimize procurement for high-loss SKUs  
- ❄️ Increase marketing/promos in Winter  

---

## 🚀 How to Use

1. Clone or download the repo  
2. Run Python script to clean and analyze data  
3. Execute SQL query for profitability metrics  
4. Open Tableau dashboard file for visual insights  

---

## 🛡 License

This project is for academic and portfolio demonstration purposes only.  
No commercial use permitted.

---

> 📌 *Created by Divisha Singh – Feel free to fork & star this repo!
