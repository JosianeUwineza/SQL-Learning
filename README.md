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
`CREATE DATABASE pixar_classic_movies`
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

   
