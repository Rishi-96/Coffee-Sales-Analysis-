# ☕ Coffee Sales Analysis using Python

## 📄 Overview

This project performs a **comprehensive analysis of coffee shop sales
data** using Python.\
The goal is to analyze transaction-level data to extract actionable
insights on sales performance, customer behavior, and product trends.\
The analysis covers all major data analytics steps --- from **data
cleaning and preprocessing** to **exploratory data analysis (EDA)**,
**KPI extraction**, **data visualization**, and **key business
insights**.

------------------------------------------------------------------------

## 🧠 Project Objectives

1.  Clean and preprocess raw transactional data for analysis.\
2.  Perform detailed exploratory data analysis (EDA) to uncover trends
    and relationships.\
3.  Calculate key performance indicators (KPIs) such as total sales,
    average order value, and top-performing stores/products.\
4.  Visualize sales trends by day, time, category, and location using
    **Matplotlib** and **Seaborn**.\
5.  Derive actionable insights that can guide business decisions.

------------------------------------------------------------------------

## 🗂️ Dataset Information

**File Name:** `Coffee Shop Sales.csv`

**Columns:** - `transaction_id`: Unique transaction identifier\
- `transaction_date`: Date of the transaction\
- `transaction_time`: Time of the transaction\
- `transaction_qty`: Quantity of items sold\
- `store_id`: Store identifier\
- `store_location`: Location of the store\
- `product_id`: Product identifier\
- `unit_price`: Price per unit\
- `product_category`: Category of the product\
- `product_type`: Type of product\
- `product_detail`: Detailed product description

------------------------------------------------------------------------

## ⚙️ Step 1: Import Libraries

``` python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

------------------------------------------------------------------------

## 🧹 Step 2: Load and Inspect Data

``` python
df = pd.read_csv("Coffee Shop Sales.csv")
df.info()
df.head()
```

------------------------------------------------------------------------

## 🧽 Step 3: Data Cleaning & Preprocessing

``` python
# Handle missing values
df.isnull().sum()

# Convert date and time columns
df['transaction_date'] = pd.to_datetime(df['transaction_date'])
df['transaction_time'] = pd.to_datetime(df['transaction_time'], format='%H:%M:%S').dt.time

# Create new columns
df['Month'] = df['transaction_date'].dt.month_name()
df['Day'] = df['transaction_date'].dt.day
df['Weekday'] = df['transaction_date'].dt.day_name()

# Extract hour from time
df['Hour'] = pd.to_datetime(df['transaction_date']).dt.hour

# Create total sales column
df['Sales'] = df['unit_price'] * df['transaction_qty']

# Remove duplicates
df.drop_duplicates(inplace=True)
```

------------------------------------------------------------------------

## 📊 Step 4: Exploratory Data Analysis (EDA)

### 4.1 Overall KPIs

``` python
total_sales = df['Sales'].sum()
total_transactions = df['transaction_id'].nunique()
avg_order_value = df['Sales'].mean()
total_qty_sold = df['transaction_qty'].sum()

print(f"Total Sales: ₹{total_sales}")
print(f"Total Transactions: {total_transactions}")
print(f"Average Order Value: ₹{avg_order_value}")
print(f"Total Quantity Sold: {total_qty_sold}")
```

------------------------------------------------------------------------

### 4.2 Monthly and Daily Sales Trends

``` python
monthly_sales = df.groupby('Month')['Sales'].sum().sort_values(ascending=False)
plt.figure(figsize=(10,5))
sns.barplot(x=monthly_sales.index, y=monthly_sales.values, palette='viridis')
plt.title("Monthly Sales Trend")
plt.xticks(rotation=45)
plt.show()
```

``` python
daily_sales = df.groupby('Weekday')['Sales'].sum()
plt.figure(figsize=(8,4))
sns.barplot(x=daily_sales.index, y=daily_sales.values, palette='coolwarm')
plt.title("Sales by Weekday")
plt.show()
```

------------------------------------------------------------------------

### 4.3 Store Performance

``` python
store_sales = df.groupby('store_location')['Sales'].sum().sort_values(ascending=False)
plt.figure(figsize=(8,4))
sns.barplot(x=store_sales.index, y=store_sales.values, palette='cubehelix')
plt.title("Store-wise Sales Performance")
plt.show()
```

------------------------------------------------------------------------

### 4.4 Top Product Categories

``` python
category_sales = df.groupby('product_category')['Sales'].sum().sort_values(ascending=False)
plt.figure(figsize=(10,5))
sns.barplot(x=category_sales.index, y=category_sales.values, palette='mako')
plt.title("Top Product Categories by Sales")
plt.xticks(rotation=45)
plt.show()
```

------------------------------------------------------------------------

### 4.5 Hourly Sales Pattern

``` python
hourly_sales = df.groupby('Hour')['Sales'].sum()
plt.figure(figsize=(8,4))
sns.lineplot(x=hourly_sales.index, y=hourly_sales.values, marker='o', color='green')
plt.title("Hourly Sales Distribution")
plt.show()
```

------------------------------------------------------------------------

### 4.6 Correlation Heatmap

``` python
plt.figure(figsize=(8,5))
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap='YlGnBu')
plt.title("Correlation Heatmap")
plt.show()
```

------------------------------------------------------------------------

## 💡 Step 5: Key Insights

1.  **Sales Peak Hours:** Most sales occur during morning and evening
    hours, aligning with coffee demand spikes.\
2.  **Best Performing Stores:** Urban and downtown store locations
    generate the highest revenue.\
3.  **Top Products:** Coffee beverages and bakery items are leading
    sales categories.\
4.  **Day-wise Trends:** Weekends show a notable increase in
    transactions compared to weekdays.\
5.  **Pricing & Sales:** Moderate unit prices correlate with higher
    transaction quantities.

------------------------------------------------------------------------

## 🧰 Tools & Libraries Used

-   **Python 3.x**\
-   **Pandas** -- Data Cleaning & Preprocessing\
-   **Matplotlib** -- Data Visualization\
-   **Seaborn** -- Exploratory Data Analysis

------------------------------------------------------------------------

## 🧾 Conclusion

This project demonstrates **end-to-end data analysis** using Python for
real-world retail data.\
It covers all essential analytical processes from cleaning and
transformation to insight generation, showcasing practical skills for a
**Data Analyst** portfolio project.

------------------------------------------------------------------------

## 📌 Author

**Rishi Jain** -- Data Analyst Enthusiast\
📍 Pune, India
