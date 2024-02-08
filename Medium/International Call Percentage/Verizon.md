```SQL
-- Calculate the percentage of international calls (phone calls where the caller and receiver are from different countries)
SELECT
    ROUND(100.0 * COUNT(pc.caller_id) /
          (SELECT COUNT(*) FROM phone_calls), 1) 
          AS percentage_different_country_calls -- Calculate the percentage of phone calls where the caller and receiver are from different countries
FROM
    phone_calls AS pc
JOIN
    phone_info AS a 
    ON pc.caller_id = a.caller_id -- Join phone_calls with phone_info to get caller information
JOIN
    phone_info AS b 
    ON pc.receiver_id = b.caller_id -- Join phone_calls with phone_info again to get receiver information
WHERE
    a.country_id != b.country_id; -- Filter only those rows where the caller and receiver are from different countries

```

```SQL
--Alternate Method Using CTE
-- Calculate the percentage of international calls (phone calls where the caller and receiver are from different countries)
WITH international_calls AS (
    SELECT
        pc.caller_id,
        a.country_id AS caller_country,
        b.country_id AS receiver_country
    FROM
        phone_calls AS pc
    JOIN
        phone_info AS a ON pc.caller_id = a.caller_id -- Join phone_calls with phone_info to get caller information
    JOIN
        phone_info AS b ON pc.receiver_id = b.caller_id -- Join phone_calls with phone_info again to get receiver information
    WHERE
        a.country_id != b.country_id -- Filter only those rows where the caller and receiver are from different countries
)
SELECT
    ROUND(100.0 * COUNT(*) / (SELECT COUNT(*) FROM phone_calls), 1) AS percentage_different_country_calls -- Calculate the percentage of phone calls where the caller and receiver are from different countries
FROM
    international_calls;
```
