```SQL
-- Common Table Expression (CTE) to prepare ranked data based on sales quantity and rating within each category
WITH ranked_products AS (
    SELECT 
        prd.product_id,
        product_name,
        category_name,
        sales_quantity,
        rating,
        RANK() OVER (PARTITION BY category_name ORDER BY sales_quantity DESC, rating DESC) AS rk
    FROM 
        products AS prd
    INNER JOIN 
        product_sales AS ps ON prd.product_id = ps.product_id
)
-- Main query to select the top-ranked product in each category
SELECT 
    category_name,
    product_name
FROM 
    ranked_products
WHERE 
    rk = 1;

```
