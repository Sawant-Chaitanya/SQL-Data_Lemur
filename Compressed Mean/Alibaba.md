```SQL
-- Calculate the mean (average) of item_count multiplied by order_occurrences, rounded to one decimal place
-- for the items_per_order table
SELECT 
    ROUND((SUM(item_count * order_occurrences) / SUM(order_occurrences))::numeric, 1) as mean
FROM 
    items_per_order;

```
