# 🛍️ H&M Insights - Power BI Sales Dashboard

[![Hero Banner](images/banner.png)](https://github.com/user-attachments/assets/1a01b202-7984-4415-8ec4-47a01d9440a8)


A powerful and interactive Power BI dashboard project built using the **H&M Personalized Fashion Recommendations dataset**. This dashboard provides visual business insights into H&M’s fashion retail strategy, covering key areas such as revenue performance, customer demographics, product trends, and channel analysis.

---

## ✨ Features & Dashboard Overview

This Power BI dashboard offers a comprehensive view of H&M's sales data, including:

* 📈 **Key Performance Indicators (KPIs):** At-a-glance metrics for total Revenue, Orders, and Customers.
* 👕 **Top Selling Product Types:** Identification of best-performing product categories.
* 🛒 **Channel-wise Sales Split:** Analysis of sales distribution between Online and Store channels.
* 🧑‍🤝‍🧑 **Customer Demographics:** Insights into customer age distribution.
* 📦 **Product Category Performance:** Understanding the popularity of different product categories (e.g., sales by gender category).
* 📆 **Sales Trends Over Time:** Visualization of sales performance over the latest six months.

---

## 🚀 Technologies Used

* **Power BI Desktop:** For data modeling, transformations, DAX calculations, and visualization.
* **DAX (Data Analysis Expressions):** For creating custom measures and calculated columns.
* **H&M Personalized Fashion Recommendations Dataset:** The primary data source.

---

## 🗂️ Dataset

The dataset used for this project is the **H&M Personalized Fashion Recommendations** dataset, available from:

* **Source:** [Hugging Face – H&M Personalized Fashion Recommendations](https://huggingface.co/datasets/dinhlnd1610/HM-Personalized-Fashion-Recommendations)

### Included Tables:

* `customers`: Contains customer demographics and behavioral data.
* `articles`: Provides metadata for various products (articles).
* `transactions`: Records all sales transactions, filtered for the **latest 6 months** for this analysis.

---

## 📌 Data Modeling & Transformations

Effective data modeling and preprocessing were crucial for creating an insightful dashboard.

### 🔗 Relationships

The following relationships were established to link the tables:

* `transactions[customer_id]` **(Many)** → **(One)** `customers[customer_id]`
* `transactions[article_id]` **(Many)** → **(One)** `articles[article_id]`

### 🧹 Preprocessing & Derived Columns

Key data preprocessing steps included:

* **Date Filtering:** `transactions` data was filtered to include only the **latest 6 months** of sales records to ensure relevance.
* **Derived Column - `Age Band`:** Customers were categorized into age groups for demographic analysis (e.g., `<20`, `20–29`, `30–39`, `40–49`, `50+`).
* **Derived Column - `Postal Prefix`:** The first three digits of the postal code were extracted for potential geographical insights.
* **Data Cleaning:** Columns with high missing values (e.g., `FN`, `Active`) were cleaned or excluded.
* **Performance Optimization:** Only essential columns were retained to optimize dashboard performance.

---

## 📊 Visualizations Breakdown

Here's a detailed look at the key visualizations within the dashboard:

### 1. 🧮 KPI Cards

![KPIs Screenshot](images/kpi_cards.png)

* **Purpose:** Provide immediate high-level overview of critical business metrics.
* **Metrics Displayed:**
    * **Customers:** Total unique customers served.
    * **Revenue:** Total revenue generated from sales.
    * **Orders:** Total number of transactions recorded.

### 2. 🛍️ Online vs Store Sales Split

![Channel Split](images/channel_split.png)

* **Visual Type:** Clustered Bar Chart
* **Fields:** `sales_channel_id` (representing Online/Store), `Total Revenue`
* **Purpose:** Analyze the distribution of sales revenue across different sales channels.

### 3. 🎯 Sales by Product Category (Gender-Specific)

![Gender Pie Chart](images/gender_category.png)

* **Visual Type:** Donut Chart
* **Axis:** `product_type_name`
* **Purpose:** Understand the popularity and revenue contribution of different product categories.

### 4. 👨‍👩‍👧‍👦 Customer Age Band Distribution

![Age Distribution](images/age_distribution.png)

* **Visual Type:** Bar Chart
* **Grouped By:** Derived `Age Band` column
* **Purpose:** Visualize the demographic spread of customers by age group.

### 5. ⏳ Total Sales Over Time

![Sales Over Time](images/sales_trend.png)

* **Visual Type:** Line Chart
* **Axis:** `transaction_date` (aggregated by month)
* **Value:** `SUM(price)`
* **Purpose:** Track sales performance and identify trends or seasonality over the selected period.
* **Note**: For more advanced time-intelligence (e.g., YTD, MTD), a dedicated date table would be beneficial in future iterations.

### 6. 🥇 Top Selling Product Types

![Top Selling Products](images/top_products.png)

* **Visual Type:** Stacked Column Chart
* **Axis:** `product_type_name`
* **Value:** `Total Revenue`
* **Features:** Sorted in descending order by `Total Revenue` and word wrap enabled for longer product names for better readability.
* **Purpose:** Highlight the product types generating the most revenue.

---

## 🧠 DAX Measures & Calculated Columns Used

The following DAX (Data Analysis Expressions) formulas were used to create key metrics and derived attributes:

```dax
-- Measures
Total Revenue = SUM(transactions[price])
Units Sold = COUNT(transactions[article_id])

-- Calculated Columns (in Customers table)
Age Band = 
    SWITCH(
        TRUE(),
        customers[age] < 20, "<20",
        customers[age] < 30, "20–29",
        customers[age] < 40, "30–39",
        customers[age] < 50, "40–49",
        "50+"
    )

-- Calculated Columns (in Customers table)
Postal Prefix = LEFT(customers[postal_code], 3)
