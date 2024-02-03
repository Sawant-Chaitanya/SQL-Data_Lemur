```SQL
--finding top two highest-grossing products within each category in the year 2022. 
WITH ranked_products AS (
  -- Filter data for transactions in the year 2022
  SELECT
    category,
    product,
    SUM(spend) AS total_spend,
    -- Assign dense rank within each category based on descending total spend
    DENSE_RANK() OVER (PARTITION BY category ORDER BY SUM(spend) DESC) AS rank
  FROM product_spend
  WHERE EXTRACT(YEAR FROM transaction_date) = 2022
  -- Group data by category and product
  GROUP BY category, product
)
-- Select top 2 highest-grossing products (adjust rank <= 2 if needed)
SELECT
  category,
  product,
  total_spend
FROM ranked_products
WHERE rank <= 2;

```
