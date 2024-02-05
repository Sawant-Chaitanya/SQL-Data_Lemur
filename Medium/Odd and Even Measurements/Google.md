```SQL
-- Common Table Expression (CTE) to prepare data with row numbers
WITH sts AS (
    SELECT 
        CAST(measurement_time AS DATE) AS measurement_day,
        measurement_value,
        ROW_NUMBER() 
            OVER (PARTITION BY CAST(measurement_time AS DATE)  ORDER BY measurement_time) AS rk
    FROM measurements
)
-- Main query to calculate the sum of odd and even row-numbered measurements for each day
SELECT 
    measurement_day,
    SUM(CASE WHEN rk % 2 != 0 THEN measurement_value else 0 END) AS odd_sum,
    SUM(CASE WHEN rk % 2 = 0 THEN measurement_value else 0 END) AS even_sum
FROM sts
GROUP BY measurement_day;
```
