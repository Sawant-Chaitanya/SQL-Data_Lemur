```SQL
-- Selecting age_bucket, and calculating the percentage of time spent sending snaps for each age group
-- and the percentage of time spent opening snaps for each age group
SELECT  
    ag.age_bucket,
    ROUND(
        (SUM(CASE WHEN at.activity_type = 'send' THEN at.time_spent END) /
         SUM(CASE WHEN at.activity_type IN ('open', 'send') THEN at.time_spent END)) * 100.0
    , 2) AS send_perc,
    ROUND(
        (SUM(CASE WHEN at.activity_type = 'open' THEN at.time_spent END) /
         SUM(CASE WHEN at.activity_type IN ('open', 'send') THEN at.time_spent END)) * 100.0
    , 2) AS open_perc
FROM 
    -- Joining the activities table with the age_breakdown table on user_id
    activities AS at
INNER JOIN 
    age_breakdown AS ag ON at.user_id = ag.user_id
GROUP BY 
    -- Grouping the results by age_bucket
    ag.age_bucket;
```

```SQL
--- Alternate way
-- Common Table Expression (CTE) named 'opt' is created to join the 'activities' and 'age_breakdown' tables based on user_id
WITH opt AS (
    SELECT 
        at.user_id,
        at.activity_type,
        at.time_spent,
        ag.age_bucket
    FROM 
        activities AS at
    INNER JOIN 
        age_breakdown AS ag ON at.user_id = ag.user_id
)

-- Main query to calculate the percentages of time spent sending and opening snaps for each age group
SELECT  
    age_bucket,
    ROUND(
        -- Calculate the percentage of time spent sending snaps for each age group
        (SUM(CASE WHEN activity_type = 'send' THEN time_spent ELSE null END) /
         SUM(CASE WHEN activity_type IN ('open', 'send') THEN time_spent ELSE null END)) * 100.0
    , 2) AS send_perc,
    ROUND(
        -- Calculate the percentage of time spent opening snaps for each age group
        (SUM(CASE WHEN activity_type = 'open' THEN time_spent ELSE null END) /
         SUM(CASE WHEN activity_type IN ('open', 'send') THEN time_spent ELSE null END)) * 100.0
    , 2) AS open_perc
FROM 
    -- Using the 'opt' CTE to perform calculations
    opt
GROUP BY 
    -- Grouping the results by age_bucket
    age_bucket;

```
