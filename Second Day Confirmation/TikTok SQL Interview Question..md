```SQL
-- Select user_id from emails and texts tables where signup action is confirmed
-- and the action date in texts is 1 day after the signup date in emails
SELECT 
  e.user_id
FROM 
  emails AS e
INNER JOIN 
  texts AS t ON t.email_id = e.email_id
WHERE 
    t.signup_action = 'Confirmed'
    AND 
    t.action_date = e.signup_date::timestamp + INTERVAL '1 day';
```
