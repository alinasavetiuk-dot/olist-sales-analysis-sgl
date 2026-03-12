# E-commerce Sales Analysis (SQL)

## Project Overview

This project analyzes e-commerce sales data from 2017 using SQL.  
The goal of the analysis is to understand revenue performance, customer behavior, product category performance, and geographic distribution of sales.

The analysis focuses on key business metrics such as revenue, number of orders, customer retention, and product category performance.

---

# Dataset

The dataset contains information about:

- orders
- order items
- products
- customers
- product categories

The data was joined and filtered to include **delivered orders from 2017** in order to perform consistent yearly analysis.

---

# Data Preparation

A temporary table was created to combine relevant information from multiple tables:

- orders
- order items
- products
- customers
- category translations

This table was used as the base dataset for all further analysis.

Main operations included:

- joining multiple tables
- filtering orders by year
- selecting relevant attributes for analysis

---

# Key Metrics (KPI)

| Metric | Value |
|------|------|
| Total Revenue | 5,964,200 |
| Total Orders | 43,428 |
| Total Customers | 42,136 |
| Average Order Value | 137.34 |

**Insight**

The platform generated **5.96M in revenue from more than 43K orders**, with an average order value of **137.34**.

---

# Revenue Analysis

## Monthly Revenue

Revenue increases gradually throughout the year and peaks in **November**, followed by strong sales in **December**.

**Insight**

The sharp spike in November likely reflects **Black Friday promotions**, followed by strong demand during the **holiday shopping season**.

---

## Revenue Growth Drivers

Although revenue grows significantly during the year, **Average Order Value remains relatively stable**.

**Insight**

Revenue growth is primarily driven by **an increase in order volume rather than customers purchasing more expensive products**.

---

# Product Category Analysis

Top revenue-generating categories include:

- bed_bath_table
- watches_gifts
- health_beauty
- sports_leisure
- computers_accessories

**Insight**

Revenue is distributed across multiple lifestyle-oriented categories, suggesting diversified consumer demand.

---

## Pareto Effect

The top **10 product categories generate more than 60% of total revenue**.

**Insight**

A relatively small portion of product categories drives the majority of platform revenue.

---

# Customer Analysis

| Metric | Value |
|------|------|
| Total Customers | 42,136 |
| Repeat Customers | 1,170 |
| Repeat Customer Rate | 2.78% |

**Insight**

Only **2.78% of customers made more than one purchase during the year**, indicating extremely low customer retention.

The platform relies heavily on **acquiring new customers rather than retaining existing ones**.

---

## Orders per Customer

Total orders: **43,428**  
Total customers: **42,136**

Average:

**≈ 1.03 orders per customer**

**Insight**

Most customers interact with the platform **only once during the year**.

---

# Geographic Analysis

Top revenue-generating cities include:

1. Sao Paulo  
2. Rio de Janeiro  
3. Belo Horizonte  
4. Brasilia  

**Insight**

Revenue is highly concentrated in **major metropolitan areas**, particularly **Sao Paulo**.

---

# Business Insights

The analysis highlights several key patterns:

- Revenue growth is driven mainly by **higher order volume**
- Sales show strong **seasonality in Q4**
- Customer retention is **very low**
- Revenue is concentrated in a limited number of product categories
- Sales are concentrated in large metropolitan areas

---

# Business Recommendations

## Improve Customer Retention

Since repeat purchases are extremely low, the company could improve retention through:

- loyalty programs
- personalized discounts
- remarketing campaigns
- email marketing

Even small improvements in retention could significantly increase revenue.

---

## Focus on High-Performing Categories

Expanding and promoting top categories could increase sales:

- home goods
- beauty products
- sports and leisure
- gifts

---

## Prepare for Seasonal Demand

Since a large share of revenue occurs in Q4, the company should:

- increase inventory before peak periods
- optimize logistics capacity
- run targeted marketing campaigns before holidays

---

## Focus on Major Urban Markets

Marketing and logistics strategies should prioritize major cities where most demand is concentrated.

---

# SQL Code

The SQL queries used in this project can be found in:
