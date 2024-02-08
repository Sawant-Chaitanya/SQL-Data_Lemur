```SQL
-- Retrieve distinct card names along with their first issued amounts, ordered by the issued amount in descending order
SELECT DISTINCT
  card_name, -- Select the card name
  FIRST_VALUE(issued_amount) OVER(PARTITION BY card_name ORDER BY issue_year, issue_month) AS issued_amount -- Calculate the first issued amount for each card
FROM monthly_cards_issued
ORDER BY issued_amount DESC; -- Order the result set by the issued amount in descending order

```
```SQL
--Using Rank
-- Common Table Expression (CTE) to rank cards based on issue date
WITH ranked_cards AS (
  SELECT
    card_name,
    issued_amount,
    ROW_NUMBER() OVER (PARTITION BY card_name ORDER BY issue_year, issue_month) AS rn -- Rank cards within each partition by issue date
  FROM monthly_cards_issued
)
-- Select cards with the first issued amount for each card
SELECT
  card_name,
  issued_amount
FROM ranked_cards
WHERE rn = 1 -- Filter only the first issued amount for each card
ORDER BY issued_amount DESC; -- Order the result set by the issued amount in descending order

```
