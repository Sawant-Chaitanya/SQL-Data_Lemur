```SQL
-- What are the latest purchases made by each user in the 'user_transactions' table?

SELECT
  transaction_date,
  user_id,
  COUNT(product_id) AS purchase_count
FROM user_transactions AS ut
-- Find the most recent transaction date for each user using a subquery
WHERE transaction_date = (
  SELECT MAX(transaction_date)
  FROM user_transactions
  WHERE user_id = ut.user_id
)
-- Group by transaction date and user ID to count purchases
GROUP BY transaction_date, user_id
-- Order by transaction date for chronological understanding
ORDER BY transaction_date;

```
