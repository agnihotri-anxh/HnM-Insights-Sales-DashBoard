# 🧵 H&M Fashion Sales Insights Dashboard

A Power BI dashboard project created using the H&M Personalized Fashion Recommendations Dataset from Hugging Face. This project provides a deep-dive analysis into customer behavior, product performance, and sales distribution to extract actionable insights for retail decision-making.

## 📂 Dataset Overview
The dataset is sourced from [HuggingFace - dinhlnd1610/HM-Personalized-Fashion-Recommendations](https://huggingface.co/datasets/dinhlnd1610/HM-Personalized-Fashion-Recommendations) and includes:

- `articles.csv` → Information about clothing items (e.g., product name, product type)
- `customers.csv` → Customer demographics (e.g., age, club status, postal code)
- `transactions.csv` → Sales transactions (date, article_id, customer_id, price)

## 🧠 Business Objective
To build a Power BI dashboard that helps:
- Understand who the customers are
- Identify high-performing product categories
- Track sales over time
- Analyze online vs offline purchase behavior
- Enable data-driven decisions through KPIs

## 📊 Dashboard Overview
![Dashboard Overview](https://github.com/user-attachments/assets/f0fe7f79-23a6-4d23-9449-1c5513942ee8)



## 🔍 Visualizations & Their Insights

### 📌 1. Key Performance Indicators (KPIs)
| KPI | Description |
|-----|-------------|
| Customers | Total unique customers |
| Revenue | Total revenue generated from transactions |
| Orders | Total number of items sold |

These metrics give a quick snapshot of overall business health.

![KPIs](screenshots/kpis.png)

### 🛍️ 2. Online vs Store Sales Split
- **Type**: Clustered Column Chart
- **Data Used**: `transactions[sales_channel_id]`
- **Insight**: Shows the dominance of online vs physical store sales

![Sales Channel Split](screenshots/sales_split.png)

### � 3. Sales by Gender Category (Donut Chart)
- **Data Used**: Merged articles and transactions with gender-related product categories
- **Insight**: Helps identify which gender-targeted categories are performing well

![Gender Category Sales](screenshots/gender_sales.png)

### 👥 4. Customer Age Band Distribution (Bar Chart)
- **Age buckets**: <20, 20-29, 30-39, 40-49, 50+
- **Derived from**: `customers[age]` column
- **Insight**: Shows which age group is the largest audience

![Age Band Distribution](screenshots/age_band.png)

### 📈 5. Total Sales Over Time (Line Chart)
- **Based on**: `transactions[t_dat]`
- **Aggregated**: Monthly
- **Insight**: Tracks sales performance trends across months

![Sales Over Time](screenshots/sales_trend.png)

### 🧵 6. Top Selling Product Types (Bar Chart)
- **Top 10 products** by `SUM(price)`
- **Data from**: `articles[product_type_name]` joined with transactions
- **Insight**: Highlights best-selling product categories like Dresses, Trousers, Skirts, etc.

![Top Products](screenshots/top_products.png)

## 🛠️ Tools Used
| Tool | Purpose |
|------|---------|
| Power BI | Data modeling and visualization |
| Python | Data preprocessing using pandas and datasets libraries |
| DAX | KPIs and custom metrics |
| Hugging Face | Dataset source |

## ⚙️ DAX Measures Used
```dax
Total Revenue = SUM(transactions[price])

Orders = COUNT(transactions[article_id])

Customers = DISTINCTCOUNT(transactions[customer_id])

Age Band = SWITCH(TRUE(),
    customers[age] < 20, "<20",
    customers[age] < 30, "20-29",
    customers[age] < 40, "30-39",
    customers[age] < 50, "40-49",
    "50+"
)

Postal Prefix = LEFT(customers[postal_code], 3)
