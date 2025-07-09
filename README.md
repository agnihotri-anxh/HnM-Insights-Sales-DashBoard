# 🛍️ H&M Insights - Power BI Sales Dashboard

(image_d5ae67.png)](![H M Sales Insights_page-0002](https://github.com/user-attachments/assets/c8b2f82d-816e-4332-820f-a5c7afd84da4)
)

**VIEW LIVE DASHBOARD:**
* **Power BI Service:** [H&M Insights Dashboard](https://app.powerbi.com/links/IDYsmDmJmj?ctid=e09c6192-2b83-4585-8c44-13d4e615579b&pbi_source=linkShare)
* **Power BI File (.pbix):** [Download from Google Drive](https://drive.google.com/file/d/17LQ3hgAAUsyqiaLctGc9l0rCMtdADJ-n/view?usp=drive_link)


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

The dashboard, as shown in the hero banner, integrates several key visualizations to provide a comprehensive sales overview:

* **KPI Cards:** Prominently display "Customers," "Revenue," and "Orders" for quick performance tracking.
* **Online vs Store Sales Split:** A clustered bar chart (or similar) illustrating sales distribution between `sales_channel_id` (Online/Store) and `Total Revenue`.
* **Sales by Product Category (Gender-Specific):** A donut chart (or similar) showing `Total Revenue` by `product_type_name` to understand category popularity.
* **Customer Age Band Distribution:** A bar chart visualizing the demographic spread of customers, grouped by the derived `Age Band`.
* **Total Sales Over Time:** A line chart plotting `SUM(price)` against `transaction_date` (aggregated by month) to reveal sales trends.
* **Top Selling Product Types:** A stacked column chart (or similar) highlighting the `product_type_name` values with the highest `Total Revenue`, sorted in descending order.

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
