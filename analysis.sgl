-- =========================================================
-- Base KPI metrics
-- Create a reusable 2017 sales dataset for further analysis
-- =========================================================

DROP TABLE IF EXISTS tmp_sales_2017;

CREATE TEMP TABLE tmp_sales_2017 AS
SELECT
    o.order_id,
    o.customer_id,
    c.customer_unique_id,
    o.order_purchase_timestamp,
    c.customer_city,
    i.order_item_id,
    i.product_id,
    i.price,
    p.product_category_name,
    COALESCE(t.product_category_name_english, 'unknown') AS en_category_name
FROM v_orders_clean AS o
INNER JOIN v_order_items_clean AS i
    ON o.order_id = i.order_id
INNER JOIN v_products_clean AS p
    ON i.product_id = p.product_id
INNER JOIN v_customers_clean AS c
    ON o.customer_id = c.customer_id
LEFT JOIN product_category_name_translation AS t
    ON p.product_category_name = t.product_category_name
WHERE o.order_purchase_timestamp >= DATE '2017-01-01'
  AND o.order_purchase_timestamp < DATE '2018-01-01';


-- Total revenue, total orders, and average order value
SELECT
    SUM(price)::numeric(12, 2) AS total_revenue,
    COUNT(DISTINCT order_id) AS number_of_orders,
    ROUND(SUM(price)::numeric / COUNT(DISTINCT order_id), 2) AS average_order_value
FROM tmp_sales_2017;


-- =========================================================
-- Deeper business metrics
-- =========================================================

-- Monthly revenue, number of orders, and average order value
SELECT
    DATE_PART('month', order_purchase_timestamp) AS month_number,
    TRIM(TO_CHAR(order_purchase_timestamp, 'Month')) AS month_name,
    SUM(price)::numeric(12, 2) AS revenue,
    COUNT(DISTINCT order_id) AS number_of_orders,
    ROUND(SUM(price)::numeric / COUNT(DISTINCT order_id), 2) AS average_order_value
FROM tmp_sales_2017
GROUP BY
    DATE_PART('month', order_purchase_timestamp),
    TRIM(TO_CHAR(order_purchase_timestamp, 'Month'))
ORDER BY month_number;


-- Revenue by product category with share and cumulative share
WITH category_revenue AS (
    SELECT
        en_category_name AS category,
        SUM(price)::numeric(12, 2) AS revenue
    FROM tmp_sales_2017
    GROUP BY en_category_name
),
category_share AS (
    SELECT
        category,
        revenue,
        ROUND(revenue / SUM(revenue) OVER () * 100, 2) AS revenue_share_percent,
        ROUND(
            SUM(revenue) OVER (ORDER BY revenue DESC)
            / SUM(revenue) OVER () * 100,
            2
        ) AS cumulative_revenue_percent
    FROM category_revenue
)
SELECT
    category,
    revenue,
    revenue_share_percent,
    cumulative_revenue_percent
FROM category_share
ORDER BY revenue DESC;


-- Top 10 products by revenue
SELECT
    product_id,
    SUM(price)::numeric(12, 2) AS revenue_per_product
FROM tmp_sales_2017
GROUP BY product_id
ORDER BY revenue_per_product DESC
LIMIT 10;


-- =========================================================
-- Customer analysis
-- =========================================================

-- Total number of unique customers
SELECT
    COUNT(DISTINCT customer_unique_id) AS number_of_customers
FROM tmp_sales_2017;


-- Customer-level revenue, order count, and average order value
SELECT
    customer_unique_id,
    SUM(price)::numeric(12, 2) AS revenue_per_customer,
    COUNT(DISTINCT order_id) AS number_of_orders,
    ROUND(SUM(price)::numeric / COUNT(DISTINCT order_id), 2) AS average_order_value
FROM tmp_sales_2017
GROUP BY customer_unique_id
ORDER BY number_of_orders DESC, revenue_per_customer DESC;


-- Repeat customer rate:
-- share of customers who placed more than one order in 2017
WITH customer_orders AS (
    SELECT
        customer_unique_id,
        COUNT(DISTINCT order_id) AS order_count
    FROM tmp_sales_2017
    GROUP BY customer_unique_id
)
SELECT
    COUNT(*) AS total_customers,
    COUNT(*) FILTER (WHERE order_count > 1) AS repeat_customers,
    ROUND(
        COUNT(*) FILTER (WHERE order_count > 1)::numeric
        / COUNT(*) * 100,
        2
    ) AS repeat_customer_rate_percent
FROM customer_orders;


-- Top cities by revenue
SELECT
    customer_city AS city,
    SUM(price)::numeric(12, 2) AS revenue_per_city
FROM tmp_sales_2017
GROUP BY customer_city
ORDER BY revenue_per_city DESC;
