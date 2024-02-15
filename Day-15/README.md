## SQL Solution for Day 15 Challenge

<img src="/Day-15/Challenge-Day15.jpeg">

```sql

-- Create user
CREATE USER mia
WITH PASSWORD 'mia123';
 
-- Create role
CREATE ROLE analyst_emp;
 
-- Grant privileges
GRANT SELECT
ON ALL TABLES IN SCHEMA public
TO analyst_emp;
 
GRANT INSERT,UPDATE
ON employees
TO analyst_emp;
 
-- Add permission to create databases
ALTER ROLE analyst_emp CREATEDB;
 
-- Assign role to user
GRANT analyst_emp TO mia;
