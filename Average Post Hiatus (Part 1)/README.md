```SQL
-- Select user_id and calculate the days between the first and last post in 2021 for users with at least two posts
SELECT 
    user_id,
    -- Extract the number of days from the duration between the first and last post dates in 2021
    --EXTRACT(DAY FROM MAX(post_date) - MIN(post_date)) 
    DATE_PART('day', MAX(post_date) - MIN(post_date)) 
    AS days_between
FROM 
    posts
WHERE 
    EXTRACT(YEAR FROM post_date) = 2021
GROUP BY 
    user_id
HAVING 
    COUNT(DISTINCT post_date) >= 2;
```
