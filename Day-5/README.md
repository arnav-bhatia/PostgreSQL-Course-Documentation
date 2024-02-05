## SQL Solution for Day 5 Challenge

<img src="/Day-5/Challenge-Day5.png">

```sql

SELECT
title,
CASE
	WHEN rating IN ('PG','PG-13') OR length > 210 THEN 'Great rating or long (tier 1)'
	WHEN description LIKE '%Drama%' AND length > 90 THEN 'Long Drama (tier 2)'
	WHEN description LIKE '%Drama%' AND length <= 90 THEN 'Short Drama (tier 3)'
	WHEN rental_rate < 1 THEN 'Very cheap (tier 4)'
END AS tier_list
FROM film
WHERE
CASE
	WHEN rating IN ('PG','PG-13') OR length > 210 THEN 'Great rating or long (tier 1)'
	WHEN description LIKE '%Drama%' AND length > 90 THEN 'Long Drama (tier 2)'
	WHEN description LIKE '%Drama%' AND length <= 90 THEN 'Short Drama (tier 3)'
	WHEN rental_rate < 1 THEN 'Very cheap (tier 4)'
END IS NOT null
