```SQL
-- Find top 2 senders with highest message count in August 2022, optimized

WITH filtered_messages AS (
  -- Pre-filter messages for August 2022 
  SELECT sender_id, message_id
  FROM messages
  WHERE sent_date >= '2022-08-01' AND sent_date < '2022-09-01'
)
SELECT sender_id, COUNT(message_id) AS count_messages
FROM filtered_messages
GROUP BY sender_id
ORDER BY message_count DESC
LIMIT 2;
```
