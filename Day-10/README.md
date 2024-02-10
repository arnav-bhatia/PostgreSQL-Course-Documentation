## SQL Solution for Day 10 Challenge

<img src="/Day-10/Challenge-Day10.png">

```sql

CREATE VIEW films_category
    AS
    SELECT 
    title,
    name,
    length
    FROM film f
    LEFT JOIN film_category fc
    ON f.film_id=fc.film_id
    LEFT JOIN category c
    ON c.category_id=fc.category_id
    WHERE name IN ('Action','Comedy')
    ORDER BY length DESC
