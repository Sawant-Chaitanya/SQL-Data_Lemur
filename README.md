# SQL-Data_Lemur
Practice SQL questions from the Data Lemur Platform

# [Question 1: Histogram of Tweets](https://datalemur.com/questions/sql-histogram-tweets)
Twitter SQL Interview Question

## Table of Contents
* Introduction
* Dataset
* Query
* Output
* Explanation

## Introduction
The goal is to write a SQL query to obtain a histogram of tweets posted per user in 2022. The histogram will show the tweet count per user as the bucket and the number of Twitter users who fall into that bucket. In other words, the query will group the users by the number of tweets they posted in 2022 and count the number of users in each group.

## Dataset
The dataset for this project is a table of Twitter tweet data, which contains the following columns:

| Column Name | Type |
| --- | --- |
| tweet_id | integer |
| user_id | integer |
| msg | string |
| tweet_date | timestamp |

Here is an example of the input data:

| tweet_id | user_id | msg | tweet_date |
| --- | --- | --- | --- |
| 214252 | 111 | Am considering taking Tesla private at $420. Funding secured. | 12/30/2021 00:00:00 |
| 739252 | 111 | Despite the constant negative press covfefe | 01/01/2022 00:00:00 |
| 846402 | 111 | Following @NickSinghTech on Twitter changed my life! | 02/14/2022 00:00:00 |
| 241425 | 254 | If the salary is so competitive why won’t you tell me what it is? | 03/01/2022 00:00:00 |
| 231574 | 148 | I no longer have a manager. I can't be managed | 03/23/2022 00:00:00 |

## Query
The SQL query that will obtain the histogram of tweets posted per user in 2022 is:

```SQL
-- Optimized query to count users with different tweet counts in 2022
WITH user_tweet_counts AS (
    -- Calculate tweet count per user efficiently within a year
    SELECT COUNT(*) AS cnt, user_id
    FROM tweets
    WHERE tweet_date >= '2022-01-01' AND tweet_date < '2023-01-01'  -- Use range condition for better performance
    GROUP BY user_id
)
SELECT cnt AS tweet_bucket,
       COUNT(*) AS users_num
FROM user_tweet_counts
GROUP BY cnt
ORDER BY cnt;  -- Optional: Sort results by tweet count for clarity
 ```

## Output
The output of the query is:

| tweet_bucket | users_num |
| --- | --- |
| 1 | 2 |
| 2 | 1 |

This output shows that two users posted only one tweet in 2022, and one user posted two tweets in 2022. The query groups the users by the number of tweets they posted and displays the number of users in each group.


## Explanation
The query works as follows:

The query works as follows:

* First, it creates a common table expression (CTE) named user_tweet_counts that selects the user_id and the count of tweet_id for each user from the tweets table, where the tweet_date is between '2022-01-01' and '2022-12-31'. This CTE filters the data by the year 2022 and calculates the number of tweets posted by each user in that year.
* Next, it selects the cnt column from the CTE as the tweet_bucket column, and counts the user_id column from the CTE as the users_num column. This query groups the users by the cnt column and counts the number of users in each group. This query produces the histogram of tweets per user in 2022.
* Finally, it orders the result by the cnt column in ascending order. This query sorts the histogram by the tweet bucket in ascending order.


