<![CDATA[# SQL for ML Interviews

> **Interview weight:** ⭐⭐⭐⭐ — Almost always tested, even in pure ML roles.  
> **Time to study:** 6–8 hours.

---

## Why SQL Matters for ML Engineers

In production, data lives in databases, not CSVs. You'll need SQL to:
- Extract training data
- Build feature tables
- Compute metrics from logs
- Join user/item/event tables for recommendation systems

---

## Essential Concepts

### JOINs

```sql
-- INNER JOIN: Only matching rows
SELECT u.name, o.amount
FROM users u
INNER JOIN orders o ON u.user_id = o.user_id;

-- LEFT JOIN: All users, even without orders (orders columns = NULL)
SELECT u.name, COALESCE(o.amount, 0) AS amount
FROM users u
LEFT JOIN orders o ON u.user_id = o.user_id;
```

### Aggregation

```sql
-- Total revenue per customer
SELECT user_id, 
       COUNT(*) AS num_orders,
       SUM(amount) AS total_spend,
       AVG(amount) AS avg_order_value
FROM orders
GROUP BY user_id
HAVING SUM(amount) > 100  -- Filter AFTER aggregation
ORDER BY total_spend DESC;
```

### Window Functions — The Most Tested Topic

```sql
-- Rank customers by total spend
SELECT user_id, total_spend,
       RANK() OVER (ORDER BY total_spend DESC) AS spend_rank
FROM customer_revenue;

-- Running total of orders per user (sorted by date)
SELECT user_id, order_date, amount,
       SUM(amount) OVER (PARTITION BY user_id ORDER BY order_date) AS running_total
FROM orders;

-- Previous order amount (lag feature for ML)
SELECT user_id, order_date, amount,
       LAG(amount, 1) OVER (PARTITION BY user_id ORDER BY order_date) AS prev_order_amount
FROM orders;

-- Moving average (7-day window)
SELECT user_id, order_date, amount,
       AVG(amount) OVER (
           PARTITION BY user_id 
           ORDER BY order_date 
           ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
       ) AS moving_avg_7d
FROM orders;
```

### Common Table Expressions (CTEs)

```sql
-- Find users whose average order value exceeds the overall average
WITH user_avg AS (
    SELECT user_id, AVG(amount) AS avg_order
    FROM orders
    GROUP BY user_id
),
overall_avg AS (
    SELECT AVG(amount) AS global_avg FROM orders
)
SELECT u.user_id, u.avg_order
FROM user_avg u, overall_avg o
WHERE u.avg_order > o.global_avg;
```

### Building Feature Tables for ML

```sql
-- Create a feature table for churn prediction
SELECT 
    u.user_id,
    u.signup_date,
    DATEDIFF(CURRENT_DATE, u.last_login) AS days_since_login,
    COUNT(o.order_id) AS total_orders,
    SUM(o.amount) AS total_spend,
    AVG(o.amount) AS avg_order_value,
    MAX(o.order_date) AS last_order_date,
    DATEDIFF(CURRENT_DATE, MAX(o.order_date)) AS days_since_last_order,
    COUNT(DISTINCT o.category) AS unique_categories
FROM users u
LEFT JOIN orders o ON u.user_id = o.user_id
GROUP BY u.user_id, u.signup_date, u.last_login;
```

---

## Practice Problems

1. Find the top 3 products by revenue for each category.
2. Calculate month-over-month growth rate for each store.
3. Find users who made purchases in 3 consecutive months.
4. Compute retention rate: % of users who ordered in month N who also ordered in month N+1.
5. Create lag features: previous 3 order amounts for each user.

---

## Common Interview Questions

1. **Q: What's the difference between WHERE and HAVING?**
   > WHERE filters rows before aggregation. HAVING filters groups after aggregation.

2. **Q: Explain RANK vs DENSE_RANK vs ROW_NUMBER.**
   > ROW_NUMBER: unique sequential numbers (1,2,3,4). RANK: same rank for ties, skips next (1,1,3,4). DENSE_RANK: same rank for ties, no skip (1,1,2,3).

3. **Q: How would you find duplicate rows?**
   > `SELECT cols, COUNT(*) FROM table GROUP BY cols HAVING COUNT(*) > 1;`

---

## Resources

- 💻 [LeetCode SQL Problems](https://leetcode.com/problemset/database/)
- 💻 [HackerRank SQL Track](https://www.hackerrank.com/domains/sql)
- 📖 [Mode SQL Tutorial](https://mode.com/sql-tutorial/)
]]>
