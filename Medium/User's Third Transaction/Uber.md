```SQL
-- Common Table Expression (CTE) to calculate the third highest spend for each user
WITH cte_user_id AS (
    SELECT 
        user_id, 
        spend, 
        transaction_date,
        -- Use NTH_VALUE to get the third highest spend for each user, ordered by transaction_date
        NTH_VALUE(spend, 3) OVER (PARTITION BY user_id ORDER BY transaction_date) AS nth_value_spend
    FROM 
        transactions
)
-- Final query to retrieve user_id, spend, and transaction_date for the calculated nth_value_spend
SELECT 
    user_id,
    spend,
    transaction_date
FROM 
    cte_user_id
-- Filter out rows where nth_value_spend is NULL, i.e., when there are less than 3 transactions for a user
WHERE 
    nth_value_spend IS NOT NULL;
```
