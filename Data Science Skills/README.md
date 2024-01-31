```SQL
-- Efficiently find candidates with all three specified skills
WITH candidate_skills AS (
    -- Calculate skill counts per candidate efficiently
    SELECT candidate_id, COUNT(DISTINCT skill) AS skill_count
    FROM candidates
    WHERE skill IN ('Python', 'Tableau', 'PostgreSQL')
    GROUP BY candidate_id
)
SELECT candidate_id
FROM candidate_skills
WHERE skill_count = 3
ORDER BY candidate_id;
```
