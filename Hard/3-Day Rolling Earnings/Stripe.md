```SQL
-- Main query to calculate the 3-day rolling average(using range)
SELECT 
    user_id,
    transaction_date,
    -- Calculate the rolling sum of transaction amounts using SUM window function with a specified range
    SUM(SUM(amount)) OVER(
        PARTITION BY user_id 
        ORDER BY transaction_date
        RANGE BETWEEN INTERVAL '2 days' PRECEDING AND CURRENT ROW
    ) AS rolling_sum_amount
FROM 
    user_transactions
GROUP BY 
    user_id, 
    transaction_date;
```
