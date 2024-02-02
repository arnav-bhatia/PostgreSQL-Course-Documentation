## SQL Solutions

![Challenges for Day 2](Day-2/Challenges-Day2.png)

```sql
SELECT
COUNT(*) AS no_of_movies
FROM film
WHERE description LIKE '%Saga%'
AND (title LIKE 'A%' OR title LIKE '%R');

--Answer: 14

SELECT
*
FROM customer
WHERE first_name LIKE '%ER%'
AND first_name LIKE '_A%'
ORDER BY last_name DESC;

--Answer: 5 people

SELECT
*
FROM payment
WHERE (amount = 0
OR amount BETWEEN 3.99 AND 7.99)
AND payment_date BETWEEN '2020-05-01' AND '2020-05-02';

--Answer: 122
