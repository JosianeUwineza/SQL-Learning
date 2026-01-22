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
` \c database name`
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
##  SECT Query 
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
