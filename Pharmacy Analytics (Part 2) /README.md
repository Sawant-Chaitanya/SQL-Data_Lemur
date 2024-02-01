```SQL
-- Select manufacturer and calculate drug count and total loss for manufacturers with negative profit
SELECT 
    manufacturer,
    COUNT(drug) AS drug_count,
    -- Calculate absolute total loss for manufacturers with negative profit
    ABS(SUM(total_sales - cogs)) AS total_loss
FROM 
    pharmacy_sales
WHERE 
    total_sales - cogs <= 0
GROUP BY 
    manufacturer
ORDER BY 
    total_loss DESC;

```
