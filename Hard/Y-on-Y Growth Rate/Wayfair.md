```SQL
-- Common Table Expression (CTE) to calculate the total spend for each product in each year
WITH yearly_spend AS (
    SELECT
        EXTRACT(YEAR FROM transaction_date) AS year,
        product_id,
        SUM(spend) AS total_spend
    FROM
        user_transactions
    GROUP BY
        EXTRACT(YEAR FROM transaction_date),
        product_id
)
-- Main query to calculate year-on-year growth rate and format the results
SELECT
    year,
    product_id,
    total_spend AS curr_year_spend,
    LAG(total_spend) OVER (PARTITION BY product_id ORDER BY year) AS prev_year_spend, -- Get the previous year's spend using LAG function
    ROUND((total_spend - LAG(total_spend) OVER (PARTITION BY product_id ORDER BY year)) / LAG(total_spend) OVER (PARTITION BY product_id ORDER BY year) * 100, 2) AS yoy_rate -- Calculate year-on-year growth rate
FROM
    yearly_spend
ORDER BY
    product_id,
    year;

```

```SQL
---Alternate way using a subquery
-- Main query to calculate year-on-year growth rate for each product
SELECT
    year,
    product_id,
    curr_year_spend,
    -- Retrieve previous year's spend using LAG window function
    LAG(curr_year_spend) OVER (PARTITION BY product_id ORDER BY year) AS prev_year_spend,
    -- Calculate year-on-year growth rate and round to 2 decimal places
    ROUND(
        (curr_year_spend - LAG(curr_year_spend) OVER (PARTITION BY product_id ORDER BY year)) /
        LAG(curr_year_spend) OVER (PARTITION BY product_id ORDER BY year) * 100,
        2
    ) AS yoy_rate
FROM (
    -- Subquery to aggregate spend for each product and year
    SELECT
        EXTRACT(YEAR FROM transaction_date) AS year,
        product_id,
        SUM(spend) AS curr_year_spend
    FROM
        user_transactions
    GROUP BY
        EXTRACT(YEAR FROM transaction_date),
        product_id
) AS yearly_spend
-- Order results by product ID and year
ORDER BY
    product_id,
    year;

```
