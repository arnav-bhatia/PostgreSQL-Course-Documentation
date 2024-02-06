## SQL Solution for Day 6 Challenge

<img src="/Day-6/Challenge-Day6.png">

```sql

SELECT 
first_name,
last_name,
email,
country
FROM customer AS c
LEFT JOIN address AS a
ON c.address_id = a.address_id
INNER JOIN city AS ci
ON a.city_id = ci.city_id
INNER JOIN country AS co
ON ci.country_id = co.country_id
WHERE country = 'Brazil'
