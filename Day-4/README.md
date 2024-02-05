## SQL Solutions for Day 4 Challenges

<img src="/Day-4/Challenge1-Day4.png">

```sql

SELECT
LEFT(email,1) || '***' || SUBSTRING(email from POSITION('.' IN email) for 2) || '***' 
|| SUBSTRING(email from POSITION('@' IN email))
FROM customer

SELECT
'***' || SUBSTRING(email from POSITION('.' IN email)-1 for 1)
|| SUBSTRING(email from POSITION('.' IN email) for 2) || '***' 
|| SUBSTRING(email from POSITION('@' IN email))
FROM customer
```

<img src="/Day-4/Challenge2-Day4.png">

```sql

SELECT
EXTRACT(day from return_date-rental_date) AS rental_days
FROM rental
WHERE customer_id = 35

SELECT
customer_id,
ROUND(AVG(EXTRACT(day from return_date-rental_date))) AS average_days_rented
FROM rental
GROUP BY customer_id
ORDER BY average_days_rented desc
LIMIT 1

--Answer : Customer with customer_id 539 has an average rental period of six days
```
