```SQL
--Laptop vs. Mobile Viewership [New York Times SQL Interview Question]
-- Count views by device type (laptop, mobile)
SELECT
  SUM(CASE WHEN device_type = 'laptop' THEN 1 END) AS laptop_views,
  SUM(CASE WHEN device_type IN ('tablet', 'phone') THEN 1 END) AS mobile_views
FROM viewership
-- Combine mobile device types for efficient counting
WHERE device_type IN ('laptop', 'tablet', 'phone');
```
