```SQL
-- Query 1: Using MODE() WITHIN GROUP to find the mode of order occurrences
-- and retrieve item counts with that mode

-- Selecting item counts where order occurrences match the mode
SELECT item_count
FROM items_per_order
-- Filtering rows where order occurrences match the mode
WHERE order_occurrences = (
  -- Subquery to calculate the mode within the dataset
  SELECT MODE() WITHIN GROUP (ORDER BY order_occurrences DESC) 
  FROM items_per_order
)
-- Sorting the result by item count
ORDER BY item_count;
```

```SQL
-- Query 2: Using a subquery to find the item count with the maximum order occurrences
-- and retrieve item counts with that maximum occurrence

-- Selecting item counts with the maximum order occurrences
SELECT item_count AS mode
FROM items_per_order
-- Filtering rows where order occurrences match the maximum occurrence
WHERE order_occurrences = (
  -- Subquery to find the maximum order occurrences
  SELECT MAX(order_occurrences) 
  FROM items_per_order
)
-- Sorting the result by item count
ORDER BY item_count;

```
