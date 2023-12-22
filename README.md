# SQL-Query-Log
Listing my SQL skillset!

# SQL Commonly used Data Types
INT -  is used to store whole numbers
VARCHAR, NVARCHAR - used to store variable length text values
DATETIME - used to store the date and time
DECIMAL, FLOAT - DECIMAL and FLOAT datatypes are used to work with decimal values such as 10.3
BIT - to store whether something 'True' or 'False' 

# Aggregate Functions
AVG() - returns the average of a set of values<br/>
COUNT() - returns the number of rows in a database table<br/>
MAX() - returns maximum value<br/>
MIN() - returns minimum value<br/>
SUM() - returns the total sum of a numeric column

# ALTER Table
used to add, delete, or modify columns in an existing table
also used to add and drop various constraints on an existing table

**Adding columns**<br/>
ALTER TABLE table_name<br/>
ADD COLUMN new_col TYPE


Example Query:<br/>
ALTER TABLE table_name<br/>
RENAME TO new_table_name

ALTER TABLE table_name<br/>
RENAME COLUMN old_name TO new_name

ALTER TABLE table_name<br/>
ALTER COLUMN column DROP NOT NULL

# BETWEEN
selects values within a given range

SELECT COUNT column<br/>
FROM table<br/>
WHERE column BETWEEN 8 AND 9

NOT BETWEEN operator in SQL can be used to retrieve values that are outside of a specified range.

# CASE
used to create different outputs based on specified conditions.Conditional expression(similar to an IF/ELSE statement)

Example query:<br/>
SELECT student_id<br/>
CASE<br/>
    WHEN (student_id <= 100) THEN 'Top 100'
    WHEN (customer_id BETWEEN 100 AND 200) THEN 'Normal'<br/>
    ELSE 'Lateral Entry'<br/>
END AS student_class<br/>
FROM students

Another example:<br/>
SELECT<br/>
SUM(CASE <br/>
    WHEN price > 1000 THEN 1<br/>
    ELSE 0<br/>
END) AS expensive <br/>
FROM products

- This would return a summed number of everything given the value 1

# CAST
Converts one data type to another<br/>
- Must be reasonable conversion
- Ex: '5' to an integer will work, 'five' to an integer will not

Syntax:<br/>
SELECT CAST('5' AS INTEGER)

Can use in a SELECT query with a column name instead of a single instance.<br/>
Example:<br/>
SELECT CAST(date AS TIMESTAMP)<br/>
FROM table

# Changing the case of a string<br/>
**Upper Case**<br/>
SELECT UPPER(email)<br/>
FROM customer

**Lower Case**<br/>
SELECT LOWER(email)<br/>
FROM customer

**Title Case**<br/>
SELECT INITCAP(title)<br/>
FROM film

# CHECK
Creates more customized constraints that adhere to a certain condition.<br/>
Example: Making sure all inserted integer values fall below a certain threshold.

Example query:<br/>
SQL Server / Oracle / MS Access:>br/>
CREATE TABLE employees(<br/>
    emp_id SERIAL PRIMARY KEY,<br/>
    first_name VARCHAR(50) NOT NULL,<br/>
    last_name VARCHAR(50) NOT NULL,<br/>
    birthdate DATE CHECK (birthdate > '1900-01-01'),<br/>
    hire_date DATE CHECK (hire_date > birthdate),<br/>
    salary INTEGER CHECK (salary > 0)<br/>
    )<br/>
    
MySQL:<br/>
CREATE TABLE Persons (<br/>
    ID int NOT NULL,<br/>
    LastName varchar(255) NOT NULL,<br/>
    FirstName varchar(255),<br/>
    Age int,<br/>
    CHECK (Age>=18)<br/>
);<br/>
# COALESCE
- function returns the first non-null value in a list.
- Useful when querying a table that contains null values and substituting it with another value.

Example query:<br/>
SELECT<br/>
   country_id,<br/>
   name,<br/> 
   national_day,<br/>
   COALESCE(national_day, 'Unknown') AS national_day_coalesced<br/>
FROM countries<br/>
ORDER BY country_id<br/>

# COUNT/COUNT DISTINCT
COUNT function returns the number of rows that matches a specified criterion.<br/>
COUNT DISTINCT will return only the distinct number of values from a column.<br/>

SELECT COUNT(column_name) FROM table

SELECT COUNT(DISTINCT column_name)<br/>
FROM table

# CREATE TABLE
General syntax:

CREATE TABLE players(<br/>
    player_id SERIAL PRIMARY KEY,<br/>
    age INTEGER NOT NULL,<br/>
    height DECIMAL(1,2),<br/>
    weight DECIMAL(3,2)<br/>
)

Another example:<br/>
CREATE TABLE account(<br/>
  user_id SERIAL PRIMARY KEY,<br/>
  username VARCHAR(50) UNIQUE NOT NULL,<br/>
  password VARCHAR(50) NOT NULL,<br/>
  email VARCHAR(250) UNIQUE NOT NULL,<br/>
  created_on TIMESTAMP NOT NULL,<br/>
  last_login TIMESTAMP<br/>
  )

**SERIAL** - typical for the primary key to create an auto-incrementing numeric column in database systems like PostgreSQ.
**AUTO_INCREMENT** - typical for the primary key to create an auto-incrementing numeric column in database systems like  MySQL.
**INDENTITY** - typical for the primary key to create an auto-incrementing numeric column in database systems like  MS SQL.

# DELETE
deletes existing records from the table in the database.<br/>
It can delete one or more rows from the table depending on the condition given with the WHERE clause. <br/>

Syntax:<br/>
DELETE FROM table<br/>
WHERE row_id = 1

Delete rows based on their presence in other tables<br/>
Example:<br/>
DELETE FROM tableA<br/>
USING tableB<br/>
WHERE tableA.id=tableB.id

Delete all rows from a table<br/>
DELETE FROM table

# DROP
Removes a column in a table along with its indexes and constraints.<br/>

General syntax:<br/>
ALTER TABLE table_name<br/>
DROP COLUMN col_name<br/>

Check for existence to avoid error:<br/>
ALTER TABLE table_name<br/>
DROP COLUMN IF EXISTS col_name<br/>

# TRUNCATE
Modifies the data in the database. The TRUNCATE command helps us delete the complete records from an existing table in the database.<br/>

TRUNCATE TABLE table_name.<br/>

# GROUP BY
Aggregates columns per category.

Example syntax:<br/>
SELECT customer_id,SUM(amount)<br/>
FROM payment<br/>
GROUP BY customer_id<br/>
ORDER BY SUM(amount)

# HAVING
Places a filter after an aggregation has already taken place

SELECT company,SUM(sales)<br/>
FROM finance_table<br/>
WHERE company != 'Google'<br/>
GROUP BY company<br/>
HAVING SUM(sales) > 1000

# IN
Creates a condition that checks to see if a value is included in a list of multiple options.

SELECT color<br/>
FROM table WHERE color IN ('red','blue')

# INSERT
Add rows into a table<br/>
General syntax:<br/>
INSERT INTO table (column1, column2)<br/>
VALUES<br/>
(value1, value2),<br/>
(value1, value2)

Syntax for sharing values from another table:<br/>
INSERT INTO table(column1,column2)<br/>
SELECT column1,column2<br/>
FROM another_table<br/>
WHERE condition;

Note: SERIAL columns do not need to be provided a value

# JOINS (INNER/OUTER/LEFT/RIGHT) | AS Statement | UNION
A JOIN clause is used to combine rows from two or more tables, based on a related column between them.

**AS** creates an "alias" for a column or result<br/>
Example syntax:<br/>
SELECT SUM(column) AS new_name<br/>
FROM table

**INNER JOIN** keyword selects records that have matching values in both tables<br/>
Examples syntax:<br/>
SELECT * FROM TableA<br/>
INNER JOIN TableB<br/>
ON TableA.col_match = TableB.col_match

**FULL OUTER JOIN** all records when there is a match in left or right  table records.<br/>
Example syntax:<br/>
SELECT * FROM customer<br/>
FULL OUTER JOIN payment<br/>
ON customer.customer_id = payment.customer_id<br/>
WHERE customer.customer_id IS null<br/>
OR payment.payment_id IS null

**LEFT OUTER JOIN**returns all records from the left table , and the matching records from the right table. The result is 0 records from the right side, if there is no match.<br/>
(Order does matter!)

**RIGHT OUTER JOIN** The same as LEFT OUTER JOIN but reversed

**UNION and UNION ALL** The UNION operator is used to combine the result-set of two or more SELECT stateme.To allow duplicate values use UNION ALL<br/>
Essentially concatenates two results together.

Example syntax:<br/>
SELECT column_name(s) FROM table1<br/>
UNION<br/>
SELECT column_name(s) FROM table2

# LIKE/ILIKE
Performs pattern matching against string data with the use of **wildcard** characters

% - matches any sequence of characters<br/>
_ - matches any single character

LIKE is case-sensitive<br/>
Example syntax:<br/>
SELECT * FROM customer<br/>
WHERE first_name LIKE 'J%' AND last_name LIKE '%her%'

# LIMIT and TOP 
Limits the number of rows returned for a query.<br/>
LIMIT Goes at the very end of a query in database systems like MySQL.TOP is used in MS SQL server and goes at the beginning of the query <br/>

SELECT column<br/>
FROM table<br/>
ORDER BY column DESC<br/>
LIMIT 5 <br/>

SELECT TOP 5 column<br/>
FROM table<br/>
ORDER BY column DESC<br/>


# Logical Operators
Combine multiple comparison operators

AND<br/>
OR<br/>
NOT<br/>

# ORDER BY
Sorts rows based on a column value, in ascending or descending order.

SELECT column_1, column_2<br/>
FROM table<br/>
ORDER BY column_1 ASC/DESC

# REPLACE<br/>
Replace characters in a string.

SELECT REPLACE(description, 'A Astounding', 'An Astounding') AS description<br/>
FROM film

# REVERSE<br/>
Reverses the order of a string.

SELECT title, REVERSE(title)<br/> 
FROM film AS f

# SELF-JOIN

A query in which a table is joined to itself.<br/>
Useful for comparing values in a column of rows within the same table.<br/>
It is necessary to use an alias for the table.

Example syntax:<br/>
SELECT tableA.col, tableB.col<br/>
FROM table AS tableA<br/>
JOIN table AS tableB ON<br/>
tableA.some_col = tableB.other_col

# String Functions and Operators<br/>
Edits, combines and alters text data columns

Example syntax:<br/>
SELECT **LENGTH**(first_name) FROM customer<br/>
Example return: 5

SELECT title, **CHAR_LENGTH**(title)<br/>
FROM film;

SELECT first_name || last_name FROM customer<br/>
Example return: JackJohnson

SELECT first_name || ' ' || last_name<br/>
Example return: Jack Johnson

SELECT LOWER(LEFT(first_name,1)) || LOWER(last_name) || '@gmail.com'<br/>
FROM customer<br/>
Example return: jjohnson@gmail.com

SELECT CONCAT(first_name, ' ', last_name) AS full_name<br/>
FROM customer;

**POSITION**<br/>
SELECT email, POSITION('@' IN email)<br/>
FROM customer;

**STRPOS** Analogous to POSITION
SELECT email, STRPOS(email, '@')<br/>
FROM customer;

**LEFT**<br/>
SELECT LEFT(description, '50') FROM film;

**RIGHT**<br/>
SELECT RIGHT(description, '50') FROM film;

**SUBSTRING**<br/>
Extract a substring from data.

SELECT SUBSTRING(description, 10, 50) FROM film AS f;<br/>
Starting at the 10th character, the next 50 characters will be returned.

SELECT SUBSTRING(email FROM 0 FOR POSITION('@' IN email))<br/>
FROM customer;<br/>
Example return: MARY.SMITH (returns everything before '@' in the email)

Example Query: Extracting only the street name from an address.<br/>
SELECT SUBSTRING(address FROM POSITION(' ' IN address)+1 FOR LENGTH(address))<br/>
FROM address;

**TRIM**<br/>
Removes characters from the start, middle or end of a string.<br/>
TRIM([leading | trailing  | both] [characters] FROM string)

SELECT TRIM(' padded ');<br/>
Removes all whitespace from the beginning and end of a string.

**LTRIM or RTRIM**<br/>
Removes only the spaces at the beginning or end of a string, not both.<br/>
SELECT LTRIM(' padded ');

SELECT RTRIM(' padded ');

Example:<br/>
SELECT<br/>
RPAD(first_name, LENGTH(first_name)+1)<br/>
|| RPAD(last_name, LENGTH(last_name)+2, ' <') <br/>
|| RPAD(email, LENGTH(email)+1, '>') AS full_email<br/>
FROM customer;

**LPAD**<br/>
SELECT LPAD('padded', 10, '#');<br/>
Returns: ####padded<br/>
Note: Returns a character length of 10 and fills blanks space with the # symbol.

# STRING_AGG<br/>
STRING_AGG(column, separator) takes all the values of a column and concatenates them, with separator in between each value

# SubQuery

Performs a query on the results of another query

SELECT title,rental_rate<br/>
FROM film<br/>
WHERE rental_rate ><br/>
(SELECT AVG(rental_rate) FROM film)

SELECT film_id,title<br/>
FROM film<br/>
(SELECT inventory.film_id<br/>
FROM rental<br/>
INNER JOIN inventory ON inventory.inventory_id = rental.inventory_id<br/>
WHERE return_date BETWEEN '2005-05-29' AND '2005-05-30')

SELECT first_name,last_name<br/>
FROM customer AS c<br/>
WHERE EXISTS<br/>
(SELECT * FROM payment AS p<br/>
WHERE p.customer_id = c.customer_id<br/>
AND amount > 11)

# Text Search

**to_tsvector and tsquery**<br/>
SELECT to_tsvector(description)<br/>
FROM film;

SELECT title, description<br/>
FROM film<br/>
WHERE to_tsvector(title) @@ to_tsquery('elf');

# TIMESTAMPS and EXTRACT

TIME - Contains only time<br/>
DATE - Contains only date<br/>
TIMESTAMP - Contains date and time<br/>
TIMESTAMPTZ - Contains date, time, and timezone

TIMEZONE<br/>
NOW<br/>
TIMEOFDAY<br/>
CURRENT_TIME<br/>
CURRENT_DATE<br/>

**EXTRACT()** - Obtain a sub-component of a date value (year, month, day, week, or quarter)<br/>
Example syntax:<br/>
EXTRACT(YEAR FROM date_col)

SELECT EXTRACT(MONTH FROM payment_date)<br/>
AS pay_month<br/>
FROM payment

**AGE()** - Calculates and returns the current age given to a timestamp<br/>
AGE(date_col)<br/>
Example return: 13 years 1 mon 5 days 01:34:13.003423

**TO_CHAR()** - Converts data types to text<br/>
Usage:<br/>
T0_CHAR(date_col,'mm-dd-yyyy')

SELECT TO_CHAR(payment_date,'MONTH-YYYY')<br/>
FROM payment

# UPDATE
Changes values of columns in a table

General syntax:<br/>
UPDATE table<br/>
SET column1 = value1,<br/>
    column2 = value2<br/>
WHERE<br/>
    condition;

Example:<br/>
UPDATE account<br/>
SET last_login = CURRENT_TIMESTAMP<br/>
    WHERE last_login IS NULL;
    
**UPDATE join**<br/>
UPDATE TableA<br/>
SET original_col = TableB.new_col<br/>
FROM tableB<br/>
WHERE tableA.id = TableB.id

To simply return affected rows, use the RETURNING function<br/>
Example:<br/>
UPDATE account<br/>
SET last_login = created_on<br/>
RETURNING account_id,last_login

# User Defined Data Types

**ENUM**<br/>
Enumerated data types are great options to use in your database when you have a column where you want to store a fixed list of values that rarely change. Examples include the directions on a compass (i.e., north, south, east and west).

CREATE TYPE compass_position AS ENUM (<br/>
'north',<br/>
'south',<br/>
'east',<br/>
'west');

Query this as:<br/>
SELECT * <br/>
FROM pg_type<br/>
WHERE typname='compass_position';

# VIEW
Stores a specific query

Example query:<br/>
CREATE VIEW customer_info AS<br/>
SELECT first_name,last_name,address FROM customer<br/>
INNER JOIN address<br/>
ON customer.address_id = address.address_id

When you want to use this VIEW, you would simply input:<br/>
SELECT * FROM customer_info

To modify the VIEW, input CREATE OR REPLACE VIEW at the beginning of the query and then make the needed adjustments to the VIEW syntax

# WHERE
The WHERE function specifies conditions on columns for the rows to be returned.

SELECT column1, column2<br/>
FROM table<br/>
WHERE conditions (ex: name='David')

# Window Functions

**FIRST_VALUE(column)**<br/>
Returns the first value in the table or partition.

**LAST_VALUE(column)**<br/>
Returns the last value in the table or partition.

Example Syntax for FIRST_VALUE and LAST_VALUE:<br/>
SELECT year, city<br/>
FIRST_VALUE(city) OVER(ORDER BY year ASC) AS first_city,<br/>
LAST_VALUE(city) OVER(ORDER BY year ASC<br/>
RANGE BETWEEN<br/>
UNBOUNDED PRECEEDING AND<br/>
UNBOUNDED FOLLOWING)<br/>
AS last_city<br/>
FROM hosts<br/>
ORDER BY year ASC;


**ROW_NUMBER()**<br/>

SELECT col_name,<br/>
    ROW_NUMBER() OVER() AS alias<br/>
FROM table_name<br/>
ORDER BY alias;

**LAG**<br/>
Returns column's value at the row n rows before the current row.

SELECT column1, column2<br/>
LAG(column2, 1) OVER (ORDER BY column1 ASC)<br/>
FROM table<br/>
ORDER BY column1 ASC;

**LEAD**<br/>
Returns column's value at the row n rows after the current row.

WITH hosts AS (<br/>
SELECT DISTINCT year, city<br/>
FROM summer_medals)<br/>

SELECT year, city,<br/>
LEAD(city, 1) OVER (ORDER BY year ASC) AS next_city<br/>
LEAD(city, 2) OVER (ORDER BY year ASC) AS after_next_city<br/>
FROM hosts<br/>
ORDER BY year ASC;

**NTILE(n)**<br/>
Splites the data into n approximately equal pages.

WITH disciplines AS (<br/>
SELECT DISTINCT discipline<br/>
FROM summer_medals)

SELECT discipline, NTILE(15) OVER () AS page<br/>
FROM disciplines<br/>
ORDER BY page ASC;

WITH Athlete_Medals AS (<br/>
  SELECT Athlete, COUNT(*) AS Medals<br/>
  FROM Summer_Medals<br/>
  GROUP BY Athlete<br/>
  HAVING COUNT(*) > 1)<br/>
  
SELECT<br/>
  Athlete,<b/r>
  Medals,<br/>
  NTILE(3) OVER() ORDERY BY medals AS Third<br/>
FROM Athlete_Medals<br/>
ORDER BY Medals DESC, Athlete ASC;

**PARTITION BY**<br/>
Splits the table into partitions based on a column's unique values

SELECT column1, column2, column3,<br/>
LAG(column3) OVER (PARTITION BY column2<br/>
ORDER BY column2 ASC, column1 ASC)<br/>
FROM table_name<br/>
ORDER BY column2 ASC, column1, ASC<br/>

**ROW_NUMBER()**<br/>
Assigns unique numbers to rows, regardless of duplicates.

**RANK()**<br/>
Assigns the same number to rows with identical values, skipping over the next numbers in such cases.

**DENSE_RANK()**<br/>
Also assigns the same number to rows with indetical values, but doesn't skip over the next numbers.

Example syntax for ROW_NUMBER, RANK and DENSE_RANK:<br/>
SELECT country, games,<br/>
ROW_NUMBER() OVER (ORDER BY games DESC) AS row_n,<br/>
RANK() OVER (ORDER BY games DESC) AS rank_n,<br/>
DENSE_RANK() OVER (ORDER BY games DESC) AS dense_rank_n<br/>
FROM table<br/>
ORDER BY games DESC, country ASC;
