```sql
WITH possible_pizzas AS (
    SELECT
        pt1.topping_name AS topping1,
        pt2.topping_name AS topping2,
        pt3.topping_name AS topping3,
        pt1.ingredient_cost + pt2.ingredient_cost + pt3.ingredient_cost AS total_cost
    FROM
        pizza_toppings pt1
    JOIN
        pizza_toppings pt2 ON pt2.topping_name > pt1.topping_name
    JOIN
        pizza_toppings pt3 ON pt3.topping_name > pt2.topping_name
)
SELECT
    CASE
        WHEN topping1 < topping2 AND topping2 < topping3 THEN CONCAT(topping1, ',', topping2, ',', topping3)
        WHEN topping1 < topping3 AND topping3 < topping2 THEN CONCAT(topping1, ',', topping3, ',', topping2)
        WHEN topping2 < topping1 AND topping1 < topping3 THEN CONCAT(topping2, ',', topping1, ',', topping3)
        WHEN topping2 < topping3 AND topping3 < topping1 THEN CONCAT(topping2, ',', topping3, ',', topping1)
        WHEN topping3 < topping1 AND topping1 < topping2 THEN CONCAT(topping3, ',', topping1, ',', topping2)
        ELSE CONCAT(topping3, ',', topping2, ',', topping1)
    END AS pizza,
    total_cost
FROM
    possible_pizzas
ORDER BY
    total_cost DESC,
    topping1,
    topping2,
    topping3;
```

# Explanation of SQL Query

This SQL query generates all possible combinations of three toppings and calculates the total cost for each combination. It then orders the results based on total cost in descending order, breaking ties by sorting toppings in ascending order alphabetically.

## Common Table Expression (CTE): possible_pizzas

The query starts with a Common Table Expression (CTE) named `possible_pizzas`, which generates all possible combinations of three toppings.

### 1. Selecting Columns and Calculating Total Cost
```sql
SELECT
    pt1.topping_name AS topping1,
    pt2.topping_name AS topping2,
    pt3.topping_name AS topping3,
    pt1.ingredient_cost + pt2.ingredient_cost + pt3.ingredient_cost AS total_cost
```
- Selects three toppings from the `pizza_toppings` table (`pt1`, `pt2`, `pt3`).
- Calculates the total cost for each combination by summing the ingredient costs of the three toppings.

### 2. Joining Tables
```sql
FROM
    pizza_toppings pt1
JOIN
    pizza_toppings pt2 ON pt2.topping_name > pt1.topping_name
JOIN
    pizza_toppings pt3 ON pt3.topping_name > pt2.topping_name
```
- Joins the `pizza_toppings` table multiple times to generate all possible combinations of three toppings. Each join condition ensures that toppings are selected in ascending alphabetical order and are not repeated.

## Main Query

After defining the CTE `possible_pizzas`, the main query selects columns from it, constructs the pizza string, and orders the results.

### Selecting Columns and Constructing Pizza String
```sql
SELECT
    CASE
        WHEN topping1 < topping2 AND topping2 < topping3 THEN CONCAT(topping1, ',', topping2, ',', topping3)
        WHEN topping1 < topping3 AND topping3 < topping2 THEN CONCAT(topping1, ',', topping3, ',', topping2)
        WHEN topping2 < topping1 AND topping1 < topping3 THEN CONCAT(topping2, ',', topping1, ',', topping3)
        WHEN topping2 < topping3 AND topping3 < topping1 THEN CONCAT(topping2, ',', topping3, ',', topping1)
        WHEN topping3 < topping1 AND topping1 < topping2 THEN CONCAT(topping3, ',', topping1, ',', topping2)
        ELSE CONCAT(topping3, ',', topping2, ',', topping1)
    END AS pizza,
    total_cost
```
- Constructs the pizza string by concatenating the three toppings in alphabetical order, ensuring there are no repeated toppings.
- Handles different ordering scenarios to ensure toppings are listed alphabetically.

### Ordering
```sql
ORDER BY
    total_cost DESC,
    topping1,
    topping2,
    topping3;
```
- Orders the results by total cost in descending order, breaking ties by sorting toppings in ascending alphabetical order.

