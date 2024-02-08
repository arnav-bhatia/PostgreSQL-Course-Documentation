## SQL Solutions for Day 8 Challenges

<img src="/Day-8 (Midcourse Assessment)/Challenge1-Day8.png">

```sql

SELECT DISTINCT
replacement_cost
FROM film
ORDER BY replacement_cost

--Answer: 9.99
```

<img src="/Day-8 (Midcourse Assessment)/Challenge2-Day8.png">

```sql

SELECT COUNT(*),
CASE
	WHEN replacement_cost BETWEEN 9.99 AND 19.99 THEN 'low'
	WHEN replacement_cost BETWEEN 20.00 AND 24.99 THEN 'medium'
	WHEN replacement_cost BETWEEN 25.00 AND 29.99 THEN 'high'
	ELSE 'not classified'
	END AS classification
FROM film
GROUP BY classification

--Answer: 514
```

<img src="/Day-8 (Midcourse Assessment)/Challenge3-Day8.png">

```sql

SELECT
title,length,name
FROM film AS f
LEFT JOIN film_category AS fc
ON f.film_id = fc.film_id
INNER JOIN category AS ca
ON fc.category_id = ca.category_id
WHERE name = 'Drama' OR name = 'Sports'
ORDER BY length DESC

--Answer: Sports and 184
```

<img src="/Day-8 (Midcourse Assessment)/Challenge4-Day8.png">

```sql

SELECT
name, 
COUNT(name) as number_of_titles
FROM film AS f
LEFT JOIN film_category AS fc
ON f.film_id = fc.film_id
INNER JOIN category AS ca
ON fc.category_id = ca.category_id
GROUP BY name
ORDER BY number_of_titles DESC

--Answer: Sport with 74 titles
```

<img src="/Day-8 (Midcourse Assessment)/Challenge5-Day8.png">

```sql

SELECT
first_name, last_name, COUNT(*) as no_of_films
FROM actor as a
INNER JOIN film_actor as fa
ON a.actor_id = fa.actor_id
GROUP BY first_name, last_name
ORDER BY no_of_films DESC

--Answer: Susan Davis with 54 films
```

<img src="/Day-8 (Midcourse Assessment)/Challenge6-Day8.png">

```sql

SELECT
address, customer_id
FROM address AS a
LEFT JOIN customer AS c
ON a.address_id = c.address_id
WHERE customer_id IS null

--Answer: 4
```

<img src="/Day-8 (Midcourse Assessment)/Challenge7-Day8.png">

```sql

SELECT
city, sum(amount)
FROM payment AS p
LEFT JOIN customer AS c
ON p.customer_id = c.customer_id
LEFT JOIN address as a
ON c.address_id = a.address_id
LEFT JOIN city as ci
ON a.city_id = ci.city_id
GROUP BY city
ORDER BY sum DESC

--Answer: Cape Coral with a total amount of 221.55
```

<img src="/Day-8 (Midcourse Assessment)/Challenge8-Day8.png">

```sql

SELECT
country, city, sum(amount)
FROM payment AS p
LEFT JOIN customer AS c
ON p.customer_id = c.customer_id
LEFT JOIN address as a
ON c.address_id = a.address_id
LEFT JOIN city as ci
ON a.city_id = ci.city_id
LEFT JOIN country as co
ON ci.country_id = co.country_id
GROUP BY country, city
ORDER BY sum 

--Answer: United States, Tallahassee with 50.85
```

<img src="/Day-8 (Midcourse Assessment)/Challenge9-Day8.png">

```sql

SELECT
staff_id, ROUND(AVG(sum),2) as avg_revenue
FROM
(SELECT
staff_id, customer_id, sum(amount)
FROM payment
GROUP BY staff_id, customer_id) as subquery
GROUP BY staff_id

--Answer:staff_id 2 with 56.64 avg revenue per customer
```

<img src="/Day-8 (Midcourse Assessment)/Challenge10-Day8.png">

```sql

SELECT
ROUND(AVG(revenue),2)
FROM
(SELECT
EXTRACT(week from payment_date) as week, SUM(amount) as revenue
FROM payment
WHERE EXTRACT(DOW from payment_date) = 0
GROUP BY week) AS sub

--Answer: 1817.04
/*
The answer is different due to different timezones from the intructor and me.
I crosschecked the solution and it matches
*/
```

<img src="/Day-8 (Midcourse Assessment)/Challenge11-Day8.png">

```sql

SELECT title, length, replacement_cost FROM film AS f1
WHERE length >
 (SELECT AVG(length) FROM film AS f2
  WHERE f1.replacement_cost = f2.replacement_cost)
ORDER BY length
```

<img src="/Day-8 (Midcourse Assessment)/Challenge12-Day8.png">

```sql

SELECT
district, ROUND(AVG(sum),2) AS lifetime_value
FROM
(SELECT
 district, SUM(amount)
 FROM payment as p
 LEFT JOIN customer as c 
 ON p.customer_id = c.customer_id
 LEFT JOIN address as a
 ON c.address_id = a.address_id
 GROUP BY p.customer_id, district)
GROUP BY district
ORDER BY lifetime_value DESC

--Answer: Saint-Denis with 216.54
```

<img src="/Day-8 (Midcourse Assessment)/Challenge13-Day8.png">

```sql

SELECT 
    name,
    amount,
    payment_id,
    (
        SELECT SUM(amount)
        FROM payment AS p
        LEFT JOIN rental AS r ON p.rental_id = r.rental_id
        LEFT JOIN inventory AS i ON r.inventory_id = i.inventory_id
        LEFT JOIN film_category AS fc ON i.film_id = fc.film_id
        LEFT JOIN category AS c1 ON fc.category_id = c1.category_id
        WHERE c.name = c1.name
    )
FROM 
    payment AS p
LEFT JOIN 
    rental AS r ON p.rental_id = r.rental_id
LEFT JOIN 
    inventory AS i ON r.inventory_id = i.inventory_id
LEFT JOIN 
    film_category AS fc ON i.film_id = fc.film_id
LEFT JOIN 
    category AS c ON fc.category_id = c.category_id
WHERE 
    name = 'Action'
ORDER BY 
    payment_id;

--Answer: Action has a revenue of 4375.85 and its lowest payment_id is 16055
```

<img src="/Day-8 (Midcourse Assessment)/Challenge14-Day8.png">

```sql

SELECT
    title,
    name,
    SUM(amount) AS total
FROM
    payment p
LEFT JOIN
    rental r ON r.rental_id = p.rental_id
LEFT JOIN
    inventory i ON i.inventory_id = r.inventory_id
LEFT JOIN
    film f ON f.film_id = i.film_id
LEFT JOIN
    film_category fc ON fc.film_id = f.film_id
LEFT JOIN
    category c ON c.category_id = fc.category_id
GROUP BY
    name, title
HAVING
    SUM(amount) = (
        SELECT MAX(total)
        FROM (
            SELECT
                title,
                name,
                SUM(amount) AS total
            FROM
                payment p
            LEFT JOIN
                rental r ON r.rental_id = p.rental_id
            LEFT JOIN
                inventory i ON i.inventory_id = r.inventory_id
            LEFT JOIN
                film f ON f.film_id = i.film_id
            LEFT JOIN
                film_category fc ON fc.film_id = f.film_id
            LEFT JOIN
                category c1 ON c1.category_id = fc.category_id
            GROUP BY
                name, title
        ) sub
        WHERE
            c.name = sub.name
    );
```
