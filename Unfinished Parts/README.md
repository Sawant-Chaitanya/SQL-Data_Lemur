```SQL
-- Selecting unfinished assembly steps (missing finish_date)

SELECT part, assembly_step
FROM parts_assembly
WHERE finish_date IS NULL;
```
