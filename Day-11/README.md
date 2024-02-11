## SQL Solution for Day 10 Challenge

<img src="/Day-11/Challenge-Day11.png">

```sql

SELECT
SUM(amount),
DATE(payment_date) as day,
LAG(SUM(amount)) OVER(ORDER BY DATE(payment_date)) as previous_day,
SUM(amount) - LAG(SUM(amount)) OVER(ORDER BY DATE(payment_date)) as difference,
ROUND((SUM(amount) - LAG(SUM(amount)) OVER(ORDER BY DATE(payment_date)))
/
LAG(SUM(amount)) OVER(ORDER BY DATE(payment_date))*100,2) as percentage_growth
FROM payment
GROUP BY DATE(payment_date)
