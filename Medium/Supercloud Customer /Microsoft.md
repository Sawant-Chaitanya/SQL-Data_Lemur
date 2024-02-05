```SQL
-- Query to identify the company ID of Microsoft 
-- Azure Supercloud customers(a company that purchases at least one product from each product category.)

SELECT cc.customer_id
FROM customer_contracts cc
INNER JOIN products p ON cc.product_id = p.product_id

-- Group the results by customer_id
GROUP BY cc.customer_id

-- Filter the groups based on the count of distinct product categories
HAVING 
        COUNT(DISTINCT p.product_category) = 
            (
    -- Subquery: Count the distinct product categories in the entire products table
            SELECT COUNT(DISTINCT product_category)
            FROM products
            );

```
