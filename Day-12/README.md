## SQL Solution for Day 12 Challenge

<img src="/Day-12/Challenge-Day12.png">

```sql

SELECT
f1.title,
f2.title,
f2.length
FROM film f1
LEFT JOIN film f2
ON f1.length = f2.length
WHERE
f1.title!=f2.title
ORDER By f2.length DESC
