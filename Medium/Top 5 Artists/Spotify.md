```SQL
-- Common Table Expression (CTE) to identify top-ranking artists based on song count
WITH top_10_cte AS (
  SELECT 
    artists.artist_name,
    -- Assigning a dense rank to artists based on the count of their songs
    DENSE_RANK() OVER (ORDER BY COUNT(songs.song_id) DESC) AS artist_rank
  FROM 
    artists
    INNER JOIN songs ON artists.artist_id = songs.artist_id
    INNER JOIN global_song_rank AS ranking ON songs.song_id = ranking.song_id
  WHERE 
    ranking.rank <= 10
  GROUP BY 
    artists.artist_name
)

-- Selecting artists and their ranks from the top 10 CTE, filtering to include only the top 5
SELECT 
  artist_name,
  artist_rank
FROM 
  top_10_cte
WHERE 
  artist_rank <= 5;
```
