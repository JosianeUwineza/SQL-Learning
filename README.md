# SQL-Learning
This repo contains all the step that I took during the SQL learning journey 
# First day
I will be using the PostgreSQL as tools for SQL
### Installation of PostgreSQL in Linux OS
* To install use this command line: `sudo apt install postgresql`
### Open or Initialize SQL
` sudo -i -u postgres`
### Create a Database
` CREATE DATABASE name of database`
* Example:
`CREATE DATABASE pixar_classic_movies;`
### Entering in Database
` psql & \c database name`
* Example: ` \c pixar_classic_movies `
### Once in Database, Create a Table
`CREATE TABLE Name of the table( columns names of table)`
* Example:
  `CREATE TABLE movies(
  Id INT PRIMARY KEY,
  Title VARCHAR(100),
  Director VARCHAR(100),
  Year INT,
  length_minutes INT);`
* To check if your table is created: `\dt`
### Add Value in Table
`INSERT INTO names of Table VALUES( value1, value2, )`
Example:
`INSERT INTO movies VALUES
(1, 'Toy Story', 'John Lasseter', 1995, 81),
(2, E'A Bug\'s Life','John Lasseter', 1998, 95),
(3, 'Toy Story 2', 'John Lasseter' , 1999, 93),
(4, 'Monsters, Inc.' , 'Pete Docter' , 2001, 92),
(5, 'Finding Nemo', 'Andrew Stanton', 2003, 107),
(6, 'The Incredibles', 'Brad Bird', 2004, 116),
(7, 'Cars', 'John Lasseter', 2006, 117),
(8, 'Ratatouille', 'Brad Bird', 2007, 115),
(9, 'WALL-E', 'Andrew Staton', 2008, 104),
(10, 'Up', 'Pete Docter', 2009, 101);
`

### Key note
* Always add the semi columns `;` at the end of each command
* Always the commas `,` separate values
* `-# `or `(#` symbolize a continuation of command line
* `=#` this is showing that no command line is running
* If there is something line `'#` it showing that there is an error
  
# SECOND DAY
##  Query 
In this we ran to select all columns from table using `SELECT, FROM` command.
### Examples
1. Find title of each film?
* Answer:
`SELECT title FROM movies;`
2. Find derector of each film?
* Answer: `SELECT director FROM movies;`
3. Find title and year if each film?
* Answer: `SECECT title, year FROM movies; `
4. Find all the information if each film?
* Answer: `SELECT * FROM movies;`
## Queries with constraints (Pt. 1)
Now we know how to select for specific columns of data from a table, but if you had a table with a hundred million rows of data, reading through all the rows would be inefficient and perhaps even impossible.
In order to filter certain results from being returned, we need to use a WHERE clause in the query. The clause is applied to each row of data by checking specific column values to determine whether it should be included in the results or not.
### Query with Constraints
```
SELECT  column, another_column, …
FROM mytable
WHERE Condition 
       AND/ OR another_condition
       AND/ OR
```
### Useful Operators
| Operator| Condition| SQL Example|
|---------|----------|------------|
|=, !=, <, <=, >, >= | Standard Numerical Operators| col_name != 4|
| BETWEEN --AND--| Number is within in range of two values (inclusive|  	col_name BETWEEN 1.5 AND 10.5|
| NOT BETWEEN … AND …| Number is not within range of two values (inclusive)| col_name NOT BETWEEN 1 AND 10 |
| IN (…) | Number exists in a list | col_name IN (2, 4, 6)|
| NOT IN (…) |  	Number does not exist in a list |  col_name NOT IN (1, 3, 5)|

### Examples
1. Find the movie with a row id of 6: `SELECT tilte FROM movies WHERE Id=6;` 
2. Find the movies released in the year(s) between 2000 and 2010: ` SELECT title , year FROM movies WHERE year BETWEEN 2000 AND 2010; `
3. Find movies not realesed in the year(s) between 2000 and 2010: `SELECT title, year FROM movies WHERE NOT BETWEEN 2000 AND 2010;`
4.  Find the first 5 Pixar movies and their release year:   `SELECT Id, title, year FROM movies WHERE Id <= 5; `
### Other useful operators with columns containing string data

| Operator| Condition| SQL Example|
|---------|----------|------------|
| =    |Case sensitive exact string comparison (notice single equals) | col_name ='abc'|
|!= or <> | Case sensitive exact string enequality comparison | col_name ! = 'abcd' |
| LIKE| Case insensitive exact string comparison | col_name Like "ABC" this means (it includes 'abc', 'Abc, ..|
| NOT LIKE| Case insensitive exact string inequality | col_name NOT LIKE "ABCD"|
| % | Use anywhere in a string to match a squence of zero or more characters (only with LIKE or NOT LIKE| col_name LIKE "%AT%" This to mean look any string with "AT" character anywhere|
| _ |  	Used anywhere in a string to match a single character (only with LIKE or NOT LIKE | col_name LIKE "AN_" (matches "AND", but not "AN")|
| IN(...) |  	String exists in a list | col_name IN ("A", "B", "C")
| NOT IN (....) |  String does not exists in a list |  	col_name NOT IN ("D", "E", "F") |

### Examples 
1. Find all the Toy Story movies
` SELECT title FROM movies 
WHERE title LIKE '%Toy Story%'; `

2. Find all the movies directed by John Lasseter
` SELECT title, director FROM movies
WHERE director = 'John Lasseter' ;`

4. Find all the movies (and director) not directed by John Lasseter
` SELECT title , director FROM movies
WHERE director != 'John Lasseter'; `

5. Find all the WALL-* movies
` SELECT * FROM movies
WHERE title LIKE 'WALL-_' ;`
#  THIRD DAY
###  Filtering and sorting Query results 
* **DISTINCT** : It is used get unique rows in a specified column or columns, but this remove the entire 
* **ORDER BY** : It used to sort your results based on specified column name either in Ascending order (ASC) or Descending order (DSC)
* **LIMIT** : It is used to restrict number of rows (give me this number of rows)
* **OFFSET** : skip rows (pagination) (“Skip the first N rows”)
### Examples
* `SSELECT DISTINCT director FROM movies ORDERED BY director ASC ;`
* `SELECT title, year FROM movies
ORDER BY year DESC
LIMIT 4;`
* `SELECT title, year FROM movies
ORDER BY year ASC
LIMIT 5; `
* `SELECT title FROM movies
ORDER BY title ASC
LIMIT 5 OFFSET 5;`

# Fourth Day
## Multi-table queries with JOINs
### INNER JOIN 
The INNER JOIN is a process that matches rows from the first table and the second table which have the same key (as defined by the ON constraint) to create a result row with the combined columns from both tables. After the tables are joined, the other clauses we learned previously are then applied.
INNER JOIN returns only the rows that exist in both tables. If there is no match, the row is not shown.
* **Usage**
```
  SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```
* **Examples**
1.
```
SELECT m.title, b.domestic_sales, b.international_sales FROM movies m
INNER JOIN boxoffice b
ON m.id=b.movie_id
;
```
2. 
```
SELECT m.title, b.rating FROM movies m
INNER JOIN boxoffice b
ON m.id=b.movie_id 
ORDER BY b.rating DESC; 
```
3.
```
SELECT m.title, b.domestic_sales, b.international_sales FROM movies m 
INNER JOIN boxoffice b
ON m.id=b.movie_id 
WHERE b.international_sales > b.domestic_sales;
```
### LEFT JOIN
It show **ALL** rows from the LEFT table, and matching rows from the RIGHT table.If there is no match **show NULL**.
**Example**
```
SELECT b.building_name, e.role FROM buidildings b
LEFT JOIN employees e
ON b.buidling_name = e.building;
```
### RIGHT JOIN
Show ALL rows from the RIGHT table, and matching rows from the LEFT table.
### FULL JOIN
Show ALL rows from BOTH tables, whether they match or not.

### JOIN types comparison (must-know table)
| JOIN TYPE  | Results(what you Get)|
|------------|----------------------|
|INNER JOIN  | Only matching rows   |
|LEFT JOIN   | All left + matches   |
| RIGTH JOIN | All right + matches  |
| FULL JOIN  | Everything           |

##  A short note on NULLs 
* NULL means **no value** / **unknown** / **missing**
* It does NOT mean: **0** or **empty string ''** or **FALSE**
* NULL = we don’t know the value or it does not exist

### Why NULLs need special attention
Because NULL behaves differently from normal values.
* for example we can't say:
    `Salary = NULL` or `Salary != NULL`
* Instead:
` Salary IS NULL` or ` SALARY IS NOT NULL`

# FIFTH Day
## Queries with Expressions in SQL
SQL allows the use of expressions to apply calculations and transformations to column values directly with in a query. These expressions can include arithmetic operations, mathematic functions, and string or data functions , depending on database.
* Key points:
     * Expressions can be used in SELECT, WHERE, and other clauses.
     * Use aliases (AS) to make computed columns easier to understand.
     * Aliases also can be applied to column names and tables to simplify complex queries, espicially when using joins.
     * While expressions are powerful, overusing them ca reduce query readability so clear aliases are recommended

### Examples
* `SELECT title, year
FROM movies
WHERE year % 2 = 0;`
* `SELECT title, (domestic_sales + international_sales) / 1000000 AS gross_sales_millions
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id;`
# SIXTH DAY
## QUERY WITH AGGREGATE FUUNCTIONS
SQL aggregate Functions allow to summarize data accross multiple rows, such as counting records or computing minimum, maiximum, average, or total values. When no grouping specified, aggregates operate on the entire result set and return a single value.
|**Common aggregate Functions** | **Description** |
|-------------------------------|-----------------|
| COUNT(*) or COUNT(column)     | Count rows (or Non NULLS) values in a column|
|MIN(column)  | Smallest value of a column|
| MAX(column) | Largest value of a colum|
|AVG(colum)| Average value|
| SUM(column)| Total value|
`
* Note that aggregates can be applied to the groups of rows using `** GROUP BY ** ` clause. This Produces on result per unique group (e.g statistics per category or year)
* **Key Notes**:
     * Use aliases (AS) to make aggregate results readable
     * Without **GROUP BY**, aggregates summarize the entire dataset.
     * With ** GROUP BY**, aggregates summarize each group separately.

* This is how Query look like:
`SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression
GROUP BY column;`
### Examples
1. `SELECT building, SUM(years_employed) as Total_years_employed
FROM employees
GROUP BY building;`
2. `SELECT MAX(years_employed) as Max_years_employed
FROM employees;`
## SQL Queries with Aggregates: **HAVING**
When using aggragate functions with `**GROUP BY**` filtering individual rows is done with `**WHERE**`, but filtering grouped results the `**HAVING**` clause.
* **Keypoints**:
     * `WHERE` filters rows before grouping.
     * `GROUP BY` groups rows based on one or more columns.
     * `HAVING` filters the aggregated groups after grouping.
     * `HAVING` uses the same condition sysntax as `WHERE`, but it works with aggregate results.
*  This is how Query look like:
`SELECT group_by_column,
       AGG_FUNC(column) AS aggregate_result
FROM mytable
WHERE condition
GROUP BY group_by_column
HAVING group_condition;
`
### Examples
* `SELECT role, SUM(years_employed)as total_year FROM employees
GROUP BY role
HAVING role = 'Engineer';`
