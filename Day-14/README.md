## SQL Solution for Day 14 Challenge

<img src="/Day-14/Challenge-Day14.png">

```sql

CREATE OR REPLACE PROCEDURE emp_swap (emp1 INT, emp2 INT)
LANGUAGE plpgsql
AS
$$
DECLARE
salary1 DECIMAL(8,2);
salary2 DECIMAL(8,2);
position1 TEXT;
position2 TEXT;
BEGIN
--Storing Variables
SELECT salary
INTO salary1
FROM employees
WHERE emp_id = emp1;

SELECT salary
INTO salary2
FROM employees
WHERE emp_id = emp2;

SELECT position_title
INTO position1
FROM employees
WHERE emp_id = emp1;

SELECT position_title
INTO position2
FROM employees
WHERE emp_id = emp2;

--Updating Salary and Titles
UPDATE employees
SET salary = salary2
WHERE emp_id = emp1;

UPDATE employees
SET salary = salary1
WHERE emp_id = emp2;

UPDATE employees
SET position_title = position2
WHERE emp_id = emp1;

UPDATE employees
SET position_title = position1
WHERE emp_id = emp2;

COMMIT;
END;
$$

CALL emp_swap (1,2)

SELECT * FROM employees
ORDER BY 1
