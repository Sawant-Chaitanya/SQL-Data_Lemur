```SQL
-- Common Table Expression (CTE) to rank the data and calculate the total number of rows
WITH ranked_data AS (
  SELECT
    searches,
    row_number() OVER (ORDER BY searches) AS rn,
    count(*) OVER () AS total_rows
  FROM
    search_frequency
)
-- Main query to calculate the median
SELECT
  ROUND(AVG(searches), 1) AS median
FROM
  ranked_data
WHERE
  rn = total_rows / 2 OR rn = (total_rows / 2) + 1; -- Select the middle row(s) for the median calculation

 

```
