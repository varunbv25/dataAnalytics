# Task 6: Sales Trend Analysis Using Aggregations

## Description
This task focuses on analyzing sales trends using SQL aggregation functions and window functions. The analysis includes monthly and yearly revenue trends, product performance, customer lifetime value, regional sales distribution, and revenue growth calculations across the online sales database.

---

## Database Schema

### Tables Created:
- **orders**: Contains order transactions with order_id, order_date, amount, product_id, and customer_id
- **products**: Product catalog with product_id, product_name, category_id, and unit_price
- **categories**: Product categories with category_id and category_name
- **customers**: Customer information including customer_id, customer_name, region, and signup_date

---

## Query 1: Monthly Sales Trends (All Years)

### SQL Query:
```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    COUNT(DISTINCT order_id) AS order_volume,
    SUM(amount) AS total_revenue,
    ROUND(AVG(amount), 2) AS avg_order_value
FROM orders
GROUP BY EXTRACT(YEAR FROM order_date), EXTRACT(MONTH FROM order_date)
ORDER BY year, month;
```

### Results:
| year | month | order_volume | total_revenue | avg_order_value |
|------|-------|--------------|---------------|-----------------|
| 2023 | 1 | 3 | 525.50 | 175.17 |
| 2023 | 2 | 4 | 876.74 | 219.19 |
| 2023 | 3 | 3 | 890.50 | 296.83 |
| 2023 | 4 | 4 | 969.24 | 242.31 |
| 2023 | 5 | 3 | 945.25 | 315.08 |
| 2023 | 6 | 3 | 969.50 | 323.17 |
| 2023 | 7 | 3 | 843.75 | 281.25 |
| 2023 | 8 | 3 | 1146.75 | 382.25 |
| 2023 | 9 | 3 | 988.50 | 329.50 |
| 2023 | 10 | 3 | 1111.24 | 370.41 |
| 2023 | 11 | 3 | 1100.25 | 366.75 |
| 2023 | 12 | 3 | 1357.25 | 452.42 |
| 2024 | 1 | 3 | 901.50 | 300.50 |
| 2024 | 2 | 3 | 1166.75 | 388.92 |
| 2024 | 3 | 3 | 1077.75 | 359.25 |
| 2024 | 4 | 3 | 1280.25 | 426.75 |
| 2024 | 5 | 3 | 1157.50 | 385.83 |
| 2024 | 6 | 3 | 1432.75 | 477.58 |
| 2024 | 7 | 3 | 1335.75 | 445.25 |
| 2024 | 8 | 3 | 1368.75 | 456.25 |
| 2024 | 9 | 3 | 1592.25 | 530.75 |

---

## Query 2: Monthly Sales Trends for 2024

### SQL Query:
```sql
SELECT
    EXTRACT(MONTH FROM order_date) AS month,
    COUNT(DISTINCT order_id) AS order_volume,
    SUM(amount) AS total_revenue,
    ROUND(AVG(amount), 2) AS avg_order_value
FROM orders
WHERE EXTRACT(YEAR FROM order_date) = 2024
GROUP BY EXTRACT(MONTH FROM order_date)
ORDER BY month;
```

### Results:
| month | order_volume | total_revenue | avg_order_value |
|-------|--------------|---------------|-----------------|
| 1 | 3 | 901.50 | 300.50 |
| 2 | 3 | 1166.75 | 388.92 |
| 3 | 3 | 1077.75 | 359.25 |
| 4 | 3 | 1280.25 | 426.75 |
| 5 | 3 | 1157.50 | 385.83 |
| 6 | 3 | 1432.75 | 477.58 |
| 7 | 3 | 1335.75 | 445.25 |
| 8 | 3 | 1368.75 | 456.25 |
| 9 | 3 | 1592.25 | 530.75 |

---

## Query 3: Yearly Sales Summary

### SQL Query:
```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    COUNT(DISTINCT order_id) AS total_orders,
    SUM(amount) AS total_revenue,
    ROUND(AVG(amount), 2) AS avg_order_value
FROM orders
GROUP BY EXTRACT(YEAR FROM order_date)
ORDER BY year;
```

### Results:
| year | total_orders | total_revenue | avg_order_value |
|------|--------------|---------------|-----------------|
| 2023 | 38 | 11724.47 | 308.54 |
| 2024 | 27 | 11313.25 | 419.01 |

---

## Query 4: Top 10 Months by Revenue

### SQL Query:
```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_id) AS order_volume
FROM orders
GROUP BY EXTRACT(YEAR FROM order_date), EXTRACT(MONTH FROM order_date)
ORDER BY total_revenue DESC
LIMIT 10;
```

### Results:
| year | month | total_revenue | order_volume |
|------|-------|---------------|--------------|
| 2024 | 9 | 1592.25 | 3 |
| 2024 | 6 | 1432.75 | 3 |
| 2024 | 8 | 1368.75 | 3 |
| 2023 | 12 | 1357.25 | 3 |
| 2024 | 7 | 1335.75 | 3 |
| 2024 | 4 | 1280.25 | 3 |
| 2024 | 2 | 1166.75 | 3 |
| 2024 | 5 | 1157.50 | 3 |
| 2023 | 8 | 1146.75 | 3 |
| 2023 | 10 | 1111.24 | 3 |

---

## Query 5: Product Performance in First Half of 2024

### SQL Query:
```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    product_id,
    COUNT(DISTINCT order_id) AS orders,
    SUM(amount) AS revenue
FROM orders
WHERE order_date BETWEEN '2024-01-01' AND '2024-06-30'
GROUP BY EXTRACT(YEAR FROM order_date), EXTRACT(MONTH FROM order_date), product_id
ORDER BY year, month, revenue DESC;
```

### Results:
| year | month | product_id | orders | revenue |
|------|-------|------------|--------|---------|
| 2024 | 1 | 103 | 1 | 378.50 |
| 2024 | 1 | 104 | 1 | 289.00 |
| 2024 | 1 | 102 | 1 | 234.00 |
| 2024 | 2 | 102 | 1 | 523.00 |
| 2024 | 2 | 105 | 1 | 445.00 |
| 2024 | 2 | 101 | 1 | 198.75 |
| 2024 | 3 | 104 | 1 | 412.00 |
| 2024 | 3 | 103 | 1 | 367.50 |
| 2024 | 3 | 105 | 1 | 298.25 |
| 2024 | 4 | 101 | 1 | 534.00 |
| 2024 | 4 | 103 | 1 | 456.75 |
| 2024 | 4 | 102 | 1 | 289.50 |
| 2024 | 5 | 105 | 1 | 512.50 |
| 2024 | 5 | 104 | 1 | 378.00 |
| 2024 | 5 | 101 | 1 | 267.00 |
| 2024 | 6 | 102 | 1 | 598.00 |
| 2024 | 6 | 104 | 1 | 445.50 |
| 2024 | 6 | 103 | 1 | 389.25 |

---

## Query 6: Sales Trends by Category

### SQL Query:
```sql
SELECT
    EXTRACT(YEAR FROM o.order_date) AS year,
    EXTRACT(MONTH FROM o.order_date) AS month,
    c.category_name,
    COUNT(DISTINCT o.order_id) AS order_count,
    SUM(o.amount) AS total_revenue,
    ROUND(AVG(o.amount), 2) AS avg_order_value
FROM orders o
JOIN products p ON o.product_id = p.product_id
JOIN categories c ON p.category_id = c.category_id
GROUP BY EXTRACT(YEAR FROM o.order_date), EXTRACT(MONTH FROM o.order_date), c.category_name
ORDER BY year, month, total_revenue DESC;
```

### Results (Sample - 46 total records):
| year | month | category_name | order_count | total_revenue | avg_order_value |
|------|-------|---------------|-------------|---------------|-----------------|
| 2023 | 1 | Electronics | 3 | 525.50 | 175.17 |
| 2023 | 2 | Electronics | 2 | 346.74 | 173.37 |
| 2023 | 2 | Home & Garden | 1 | 310.00 | 310.00 |
| 2023 | 2 | Sports | 1 | 220.00 | 220.00 |
| 2023 | 3 | Electronics | 2 | 623.50 | 311.75 |
| 2023 | 3 | Sports | 1 | 267.00 | 267.00 |
| 2024 | 2 | Electronics | 3 | 1166.75 | 388.92 |
| 2024 | 9 | Electronics | 2 | 1079.50 | 539.75 |
| 2024 | 9 | Sports | 1 | 512.75 | 512.75 |

---

## Query 7: Sales Trends by Region

### SQL Query:
```sql
SELECT
    EXTRACT(YEAR FROM o.order_date) AS year,
    EXTRACT(MONTH FROM o.order_date) AS month,
    cu.region,
    COUNT(DISTINCT o.order_id) AS order_count,
    SUM(o.amount) AS total_revenue,
    COUNT(DISTINCT cu.customer_id) AS unique_customers
FROM orders o
JOIN customers cu ON o.customer_id = cu.customer_id
GROUP BY EXTRACT(YEAR FROM o.order_date), EXTRACT(MONTH FROM o.order_date), cu.region
ORDER BY year, month, total_revenue DESC;
```

### Results (Sample - 62 total records):
| year | month | region | order_count | total_revenue | unique_customers |
|------|-------|--------|-------------|---------------|------------------|
| 2023 | 1 | South | 1 | 200.00 | 1 |
| 2023 | 1 | East | 1 | 175.50 | 1 |
| 2023 | 1 | North | 1 | 150.00 | 1 |
| 2023 | 10 | South | 2 | 834.99 | 2 |
| 2023 | 10 | North | 1 | 276.25 | 1 |
| 2024 | 1 | North | 2 | 523.00 | 2 |
| 2024 | 1 | South | 1 | 378.50 | 1 |
| 2024 | 8 | South | 2 | 801.75 | 2 |
| 2024 | 8 | North | 1 | 567.00 | 1 |

---

## Query 8: Customer Lifetime Value Analysis

### SQL Query:
```sql
SELECT
    cu.customer_id,
    cu.customer_name,
    cu.region,
    COUNT(DISTINCT o.order_id) AS total_orders,
    SUM(o.amount) AS lifetime_value,
    ROUND(AVG(o.amount), 2) AS avg_order_value,
    MIN(o.order_date) AS first_order_date,
    MAX(o.order_date) AS last_order_date
FROM customers cu
JOIN orders o ON cu.customer_id = o.customer_id
GROUP BY cu.customer_id, cu.customer_name, cu.region
ORDER BY lifetime_value DESC;
```

### Results:
| customer_id | customer_name | region | total_orders | lifetime_value | avg_order_value | first_order_date | last_order_date |
|-------------|---------------|--------|--------------|----------------|-----------------|------------------|-----------------|
| 4 | Sarah Davis | West | 7 | 2800.00 | 400.00 | 2023-02-03 | 2024-09-18 |
| 2 | Emma Johnson | South | 7 | 2513.24 | 359.03 | 2023-01-12 | 2024-08-28 |
| 5 | David Wilson | North | 7 | 2428.74 | 346.96 | 2023-02-14 | 2024-09-26 |
| 6 | Lisa Anderson | South | 6 | 2336.25 | 389.38 | 2023-02-20 | 2024-06-24 |
| 10 | Jennifer Lopez | South | 6 | 2284.25 | 380.71 | 2023-03-22 | 2024-08-08 |
| 1 | John Smith | North | 7 | 2283.25 | 326.18 | 2023-01-05 | 2024-08-19 |
| 3 | Michael Brown | East | 7 | 2219.74 | 317.11 | 2023-01-18 | 2024-09-09 |
| 8 | Emily Martinez | West | 6 | 2181.50 | 363.58 | 2023-03-08 | 2024-07-16 |
| 9 | Robert Garcia | North | 6 | 2079.00 | 346.50 | 2023-03-15 | 2024-07-27 |
| 7 | James Taylor | East | 6 | 1911.75 | 318.63 | 2023-02-25 | 2024-07-05 |

---

## Query 9: Month-over-Month Revenue Growth Analysis

### SQL Query:
```sql
SELECT
    year,
    month,
    total_revenue,
    order_volume,
    LAG(total_revenue) OVER (ORDER BY year, month) AS prev_month_revenue,
    ROUND(
        ((total_revenue - LAG(total_revenue) OVER (ORDER BY year, month)) /
        LAG(total_revenue) OVER (ORDER BY year, month) * 100),
        2
    ) AS revenue_growth_percent
FROM (
    SELECT
        EXTRACT(YEAR FROM order_date) AS year,
        EXTRACT(MONTH FROM order_date) AS month,
        SUM(amount) AS total_revenue,
        COUNT(DISTINCT order_id) AS order_volume
    FROM orders
    GROUP BY EXTRACT(YEAR FROM order_date), EXTRACT(MONTH FROM order_date)
) monthly_data
ORDER BY year, month;
```

### Results:
| year | month | total_revenue | order_volume | prev_month_revenue | revenue_growth_percent |
|------|-------|---------------|--------------|--------------------|-----------------------|
| 2023 | 1 | 525.50 | 3 | NULL | NULL |
| 2023 | 2 | 876.74 | 4 | 525.50 | 66.84 |
| 2023 | 3 | 890.50 | 3 | 876.74 | 1.57 |
| 2023 | 4 | 969.24 | 4 | 890.50 | 8.84 |
| 2023 | 5 | 945.25 | 3 | 969.24 | -2.48 |
| 2023 | 6 | 969.50 | 3 | 945.25 | 2.57 |
| 2023 | 7 | 843.75 | 3 | 969.50 | -12.97 |
| 2023 | 8 | 1146.75 | 3 | 843.75 | 35.91 |
| 2023 | 9 | 988.50 | 3 | 1146.75 | -13.80 |
| 2023 | 10 | 1111.24 | 3 | 988.50 | 12.42 |
| 2023 | 11 | 1100.25 | 3 | 1111.24 | -0.99 |
| 2023 | 12 | 1357.25 | 3 | 1100.25 | 23.36 |
| 2024 | 1 | 901.50 | 3 | 1357.25 | -33.58 |
| 2024 | 2 | 1166.75 | 3 | 901.50 | 29.42 |
| 2024 | 3 | 1077.75 | 3 | 1166.75 | -7.63 |
| 2024 | 4 | 1280.25 | 3 | 1077.75 | 18.79 |
| 2024 | 5 | 1157.50 | 3 | 1280.25 | -9.59 |
| 2024 | 6 | 1432.75 | 3 | 1157.50 | 23.78 |
| 2024 | 7 | 1335.75 | 3 | 1432.75 | -6.77 |
| 2024 | 8 | 1368.75 | 3 | 1335.75 | 2.47 |
| 2024 | 9 | 1592.25 | 3 | 1368.75 | 16.33 |

---

## Query 10: Quarterly Product Performance Analysis

### SQL Query:
```sql
SELECT
    EXTRACT(YEAR FROM o.order_date) AS year,
    EXTRACT(QUARTER FROM o.order_date) AS quarter,
    p.product_name,
    c.category_name,
    COUNT(DISTINCT o.order_id) AS orders,
    SUM(o.amount) AS total_revenue,
    ROUND(AVG(o.amount), 2) AS avg_order_value
FROM orders o
JOIN products p ON o.product_id = p.product_id
JOIN categories c ON p.category_id = c.category_id
GROUP BY
    EXTRACT(YEAR FROM o.order_date),
    EXTRACT(QUARTER FROM o.order_date),
    p.product_name,
    c.category_name
ORDER BY year, quarter, total_revenue DESC;
```

### Results (Sample - 35 total records):
| year | quarter | product_name | category_name | orders | total_revenue | avg_order_value |
|------|---------|--------------|---------------|--------|---------------|-----------------|
| 2023 | 1 | Smart Watch | Electronics | 3 | 588.49 | 196.16 |
| 2023 | 1 | Running Shoes | Sports | 2 | 487.00 | 243.50 |
| 2023 | 1 | Wireless Headphones | Electronics | 3 | 482.25 | 160.75 |
| 2023 | 1 | Laptop Stand | Electronics | 1 | 425.00 | 425.00 |
| 2023 | 1 | Coffee Maker | Home & Garden | 1 | 310.00 | 310.00 |
| 2023 | 2 | Running Shoes | Sports | 2 | 737.00 | 368.50 |
| 2023 | 2 | Smart Watch | Electronics | 2 | 612.00 | 306.00 |
| 2023 | 2 | Laptop Stand | Electronics | 2 | 588.74 | 294.37 |
| 2023 | 2 | Coffee Maker | Home & Garden | 2 | 579.00 | 289.50 |
| 2024 | 1 | Smart Watch | Electronics | 2 | 757.00 | 378.50 |
| 2024 | 1 | Running Shoes | Sports | 2 | 746.00 | 373.00 |
| 2024 | 1 | Laptop Stand | Electronics | 2 | 743.25 | 371.63 |
| 2024 | 1 | Coffee Maker | Home & Garden | 2 | 701.00 | 350.50 |
| 2024 | 2 | Smart Watch | Electronics | 2 | 887.50 | 443.75 |
| 2024 | 2 | Running Shoes | Sports | 2 | 846.00 | 423.00 |
| 2024 | 3 | Wireless Headphones | Electronics | 2 | 1101.75 | 550.88 |
| 2024 | 3 | Smart Watch | Electronics | 2 | 990.50 | 495.25 |
| 2024 | 3 | Running Shoes | Sports | 2 | 925.25 | 462.63 |

---

## Key Insights

1. **Revenue Growth**: The average order value increased from $308.54 in 2023 to $419.01 in 2024, showing a 35.8% improvement.

2. **Peak Months**: September 2024 had the highest revenue at $1,592.25, followed by June 2024 ($1,432.75).

3. **Customer Value**: Sarah Davis has the highest lifetime value at $2,800.00, followed by Emma Johnson at $2,513.24.

4. **Category Performance**: Electronics consistently generates the highest revenue across all time periods.

5. **Regional Distribution**: Sales are distributed across four regions (North, South, East, West) with varying performance.

6. **Growth Volatility**: Month-over-month growth shows significant variation, ranging from -33.58% to +66.84%.
