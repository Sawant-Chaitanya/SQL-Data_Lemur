```SQL
-- Select card_name and calculate the difference between the maximum and minimum issued_amount
-- for each card_name in the monthly_cards_issued table
SELECT 
    card_name,
    MAX(issued_amount) - MIN(issued_amount) AS difference
FROM 
    monthly_cards_issued
GROUP BY 
    card_name
ORDER BY 
    difference DESC;

```
