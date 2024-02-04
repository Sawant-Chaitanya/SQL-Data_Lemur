```SQL
-- Calculating the conversion rate of confirmed signups based on emails and texts
SELECT 
  -- Using ROUND to round the result to two decimal places
  ROUND(
    -- Calculating the ratio of confirmed signups to total signups
    SUM(CASE WHEN t.signup_action = 'Confirmed' THEN 1 ELSE 0 END) * 1.0 / COUNT(t.signup_action)
    -- Rounding the result to two decimal places
    , 2
  ) AS conversion_rate
FROM 
  emails AS em
  -- Performing a LEFT JOIN with texts based on email_id
  LEFT JOIN texts AS t ON em.email_id = t.email_id;

```
