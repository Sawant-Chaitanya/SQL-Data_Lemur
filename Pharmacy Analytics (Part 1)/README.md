```SQL
-- Select drug and calculate total profit for each drug, grouped by drug
SELECT 
    drug,
    -- Calculate total profit by subtracting cogs from total_sales and summing the result
    SUM(total_sales - cogs) AS total_profit
FROM 
    pharmacy_sales
GROUP BY 
    drug
ORDER BY 
    total_profit DESC
LIMIT 3;

```
