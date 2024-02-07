## SQL Solutions for Day 7 Challenges

<img src="/Day-7/Challenge1-Day7.png">

```sql

SELECT
    title,
    replacement_cost,
    rating,
    (
        SELECT ROUND(AVG(replacement_cost), 2) AS avg_cost
        FROM film AS f3
        WHERE f1.rating = f3.rating
    ) AS avg_cost
FROM
    film AS f1
WHERE
    replacement_cost IN (
        SELECT MAX(replacement_cost)
        FROM film AS f2
        WHERE f1.rating = f2.rating
    )
ORDER BY
    rating;
```

<img src="/Day-7/Challenge2-Day7.png">

```sql

SELECT
    first_name,
    payment_id,
    amount
FROM
    payment AS p1
INNER JOIN
    customer AS c ON p1.customer_id = c.customer_id
WHERE
    amount IN (
        SELECT MAX(amount)
        FROM payment AS p2
        WHERE p1.customer_id = p2.customer_id
    );
```
