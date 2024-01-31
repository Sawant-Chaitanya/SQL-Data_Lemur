```SQL
-- Select the app_id and calculate the Click-Through Rate (CTR) for each app [Facebook SQL Interview Question]
SELECT 
    app_id,
    -- Calculate CTR using ROUND function to round the result to two decimal places
    ROUND(
        100.0 * 
        (
            -- Count the number of click events
            COUNT(CASE WHEN event_type = 'click' THEN event_type ELSE NULL END)
        ) / 
        (
            -- Count the number of impression events
            COUNT(CASE WHEN event_type = 'impression' THEN event_type ELSE NULL END)
        ), 2
    ) AS ctr
FROM 
    events
WHERE 
    -- Filter events based on the timestamp to consider only events within the specified date range
    timestamp >= '2022-01-01' AND timestamp < '2023-01-01'
GROUP BY 
    app_id;
```
