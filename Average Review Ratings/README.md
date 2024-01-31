```SQL
-- Select the month, product ID, and rounded average stars for reviews
SELECT 
    EXTRACT(MONTH FROM submit_date) AS mth,
    product_id AS product,
    -- Calculate the rounded average of stars with two decimal places
    ROUND(AVG(stars), 2) AS avg_stars
FROM 
    reviews
-- Group the results by month and product ID
GROUP BY 
    EXTRACT(MONTH FROM submit_date),
    product_id
-- Order the results by month and product ID
ORDER BY 
    mth, 
    product;
```
