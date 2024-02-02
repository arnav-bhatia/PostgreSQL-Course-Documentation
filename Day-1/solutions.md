## SQL Solutions

![Challenges for Day 1](Day-1/Challenges-Day1.png)

```sql
SELECT DISTINCT
district
FROM address;

--Answer: 378

SELECT
rental_date
FROM rental
ORDER BY rental_date DESC
LIMIT 1

--Answer: 2020-2-14

SELECT
COUNT(*)
FROM film

--Answer: 1000

SELECT 
COUNT(DISTINCT last_name)
FROM customer

--Answer : 599
