```SQL
-- Selecting user_id, tweet_date, and calculating 
-- the rolling average of 3-days as tweet_count
SELECT 
    user_id,
    tweet_date,
    -- Calculating the 3-day rolling average tweet_count using the window function AVG
    ROUND(
        AVG(tweet_count) OVER (
            PARTITION BY user_id 
            ORDER BY tweet_date
            ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
        ), 2
    ) AS tweet_count
FROM 
    tweets;
```
