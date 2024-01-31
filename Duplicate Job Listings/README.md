```SQL
-- Common Table Expression (CTE) to identify duplicate job listings within the same company
WITH DuplicateJobListings AS (
    SELECT company_id
    FROM job_listings
    GROUP BY company_id, title, description
    HAVING COUNT(job_id) > 1
)

-- Select the count of companies posting duplicate job listings
SELECT COUNT(DISTINCT company_id) AS duplicate_companies
FROM DuplicateJobListings;
```
