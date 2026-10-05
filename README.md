# 🛍️ Customer Shopping Behavior Analysis

An end-to-end data analytics project that uses **Python, SQL, and Power BI** to uncover what drives customer purchases, loyalty, and subscription behavior for a retail company.

---

## 📌 Business Problem

A leading retail company has noticed shifting purchase patterns across demographics, product categories, and sales channels. Management wants to know:

> **"How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?"**

The analysis focuses on factors such as discounts, reviews, seasons, shipping, and subscription status, and how they influence spending and repeat purchases.

---

## 🧰 Tech Stack

| Stage | Tool |
|-------|------|
| Data cleaning & feature engineering | Python (pandas) |
| Data storage & analysis | SQL (PostgreSQL) |
| Visualization | Power BI |
| Reporting | PDF report |

---

## 📂 Repository Structure

```
├── data/
│   ├── customer_shopping_behavior.csv           # Raw dataset
│   └── customer_shopping_behavior_cleaned.csv   # Cleaned dataset (output of the notebook)
├── notebooks/
│   └── Customer_Shopping.ipynb                  # Python data prep & feature engineering
├── sql/
│   └── Customer_behavior_mysql_query.txt        # 10 business-question SQL queries
├── dashboard/
│   └── customer_behavior_dashboard.pbix         # Power BI dashboard
├── docs/
│   ├── Business_Problem__Document.pdf           # Problem statement & deliverables
│   └── Customer_Shopping_Behavior_Analysis.pdf  # Full project report
└── README.md
```

---

## 📊 Dataset Overview

- **Rows:** 3,900 purchase records
- **Columns:** 18 (19 after cleaning and feature engineering)
- **Feature groups:**
  - **Demographics:** age, gender, location, subscription status
  - **Purchase details:** item purchased, category, purchase amount (USD), size, color, season
  - **Behavior:** discount applied, previous purchases, purchase frequency, review rating, shipping type, payment method
- **Data quality issue:** 37 missing values in `Review Rating`

---

## 🔄 Project Workflow

### 1. Data Preparation (Python)
Performed in `Customer_Shopping.ipynb`:

- Loaded the data with `pandas` and explored it with `df.info()` and `df.describe()`
- **Imputed** 37 missing `Review Rating` values using the **median rating of each product category**
- **Standardized** column names to `snake_case` (e.g., `Purchase Amount (USD)` → `purchase_amount`)
- **Engineered features:**
  - `age_group`: customers split into four quartile-based groups (Young Adult, Adult, Middle-aged, Senior)
  - `purchase_frequency_days`: purchase frequency converted to a number of days (e.g., Weekly → 7, Quarterly → 90)
- **Dropped** `promo_code_used` after confirming it was identical to `discount_applied`
- Exported the cleaned dataset and loaded it into a SQL database for analysis

### 2. Data Analysis (SQL)
Ten business questions answered in `Customer_behavior_mysql_query.txt`:

| # | Question | Techniques |
|---|----------|-----------|
| 1 | Revenue by gender | `GROUP BY`, `SUM` |
| 2 | Discount users who spent above average | Subquery |
| 3 | Top 5 products by average rating | `AVG`, `ORDER BY`, `LIMIT` |
| 4 | Standard vs. Express shipping spend | `AVG`, `WHERE IN` |
| 5 | Subscribers vs. non-subscribers | Multi-metric aggregation |
| 6 | Top 5 most discount-dependent products | Conditional aggregation (`CASE`) |
| 7 | New / Returning / Loyal customer segments | CTE + `CASE` |
| 8 | Top 3 products per category | CTE + `ROW_NUMBER()` window function |
| 9 | Do repeat buyers subscribe? | Filtering + grouping |
| 10 | Revenue by age group | `GROUP BY`, `ORDER BY` |

### 3. Visualization (Power BI)
An interactive **Customer Behavior Dashboard** with:

- **KPI cards:** Number of customers (3.9K), average purchase amount ($59.76), average review rating (3.75)
- **Charts:** subscription split, revenue and sales by category, revenue and sales by age group
- **Slicers:** subscription status, gender, category, shipping type

---

## 🔍 Key Findings

- **Gender:** Male customers generated about **$157.9K** in revenue vs. **$75.2K** from female customers.
- **Subscriptions:** Only **27%** of customers are subscribers. Subscribers and non-subscribers spend almost the same on average ($59.49 vs. $59.87), so subscribing is not currently linked to higher spend.
- **Repeat buyers:** Of customers with more than 5 previous purchases, **958 subscribe vs. 2,518 who don't**, which suggests a large conversion opportunity.
- **Loyalty:** **3,116** customers are classified as Loyal, 701 as Returning, and only 83 as New.
- **Shipping:** Express shipping shows a slightly higher average purchase ($60.48) than Standard ($58.46).
- **Discount-heavy products:** Hat, Sneakers, Coat, Sweater, and Pants have ~47–50% of purchases made with a discount.
- **Top-rated products:** Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), Skirt (3.78).
- **Age groups:** Revenue is fairly evenly spread, with Young Adults contributing the most ($62.1K).
- **Categories:** Clothing and Accessories drive the majority of revenue and sales volume.

---

## 💡 Business Recommendations

1. **Boost subscriptions:** Promote exclusive subscriber benefits, especially to the many loyal repeat buyers who haven't subscribed yet.
2. **Loyalty programs:** Reward repeat buyers and nudge Returning customers into the Loyal segment.
3. **Review discount policy:** Balance sales lift against margin, particularly for discount-dependent products.
4. **Product positioning:** Feature top-rated and best-selling products in campaigns.
5. **Targeted marketing:** Focus on high-revenue age groups and express-shipping users.

---

## 🚀 How to Run

1. **Clone the repo**
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```
2. **Install dependencies**
   ```bash
   pip install pandas jupyter
   ```
3. **Run the notebook:** open `notebooks/Customer_Shopping.ipynb` and run all cells. This reads the raw CSV and writes the cleaned CSV.
4. **Load into SQL:** import `customer_shopping_behavior_cleaned.csv` into a database as a table named `customer`, then run the queries in the `sql/` folder.
5. **Open the dashboard:** open `customer_behavior_dashboard.pbix` in **Power BI Desktop**.

---

## 🙋 Author

**Your Name**
[LinkedIn](https://linkedin.com/in/your-profile) · [GitHub](https://github.com/your-username)
