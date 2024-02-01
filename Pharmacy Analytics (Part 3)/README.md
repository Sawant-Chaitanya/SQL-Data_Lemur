```SQL
-- Select manufacturer and calculate total units sold, rounding to the nearest million, and formatting as dollars
SELECT 
    manufacturer,
    -- Round the total units sold to the nearest million
    CONCAT('$', TO_CHAR(ROUND(SUM(total_sales) / 1000000)::numeric, 'FM999,999,999')) || ' million' AS sale
FROM 
    pharmacy_sales
GROUP BY 
    manufacturer
ORDER BY 
    SUM(total_sales) DESC, 
    manufacturer;

```
