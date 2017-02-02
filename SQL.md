# Structured Query Language (SQL)
*Notes from Codecademy's "Learn SQL"-cource.*

*SQL* is a programming language designed to manipulate and manage data stored in relational databases. SQL operates through simple, declarative statements. This keeps data accurate and secure, and helps maintain the integrity of databases, regardless of size.

See: [List of SQL commands.](https://www.codecademy.com/articles/sql-commands)

## Build Tables
- A *relational database* is a database that organizes information into one or more tables.
- A *table* is a collection of data organized into rows and columns.
- A *statement* is a string of characters that the database recognizes as a valid command.
  - `CREATE TABLE` creates a new table.
  - `INSERT INTO` adds a new row to a table.
  - `SELECT` queries data from a table.
  - `UPDATE` edits a row in a table.
  - `ALTER TABLE` changes an existing table, i.e. by adding a column.
  - `DELETE FROM` deletes rows from a table.
  
Example:
```sql
# --- Creates a table with the following columns: id, title, genre, year.
CREATE TABLE movies (
    id INTEGER, 
    title TEXT, 
    genre TEXT, 
    year INTEGER
);

# --- Insert two rows into the table.
INSERT INTO movies (id, title, genre, year, imdb_rating) 
VALUES (1, 'Seven', 'Action', 1995);
INSERT INTO movies (id, title, genre, year, imdb_rating) 
VALUES (2, 'Django Unchained', 'Western', 2012);

# --- Add a column called imdb_rating to movies. 
#     The existing movies get imdb_rating set to NULL.
ALTER TABLE movies 
ADD COLUMN imdb_rating REAL;

# --- Change the imdb_rating of the row with id = 1.
UPDATE movies 
SET imdb_rating = 8.6 
WHERE id = 1;

# --- Delete all rows where imdb_rating is NULL.
DELETE FROM movies
WHERE imdb_rating IS NULL;
```

- Some of the most common data types are:

  1. `INTEGER`, a positive or negative whole number 
  2. `TEXT`, a text string 
  3. `DATE`, the date formatted as YYYY-MM-DD for the year, month, and day 
  4. `REAL`, a decimal value 
  
## Retrieve Information from a Database by Writing Queries
  - `SELECT` is the clause you use every time you want to query information from a database.
  - `SELECT DISTINCT` specifies that the statement is going to be a query that returns unique values in the specified column(s).
  - `WHERE` is a popular command that lets you filter the results of the query based on conditions that you specify.
  - `LIKE` and `BETWEEN` are special operators that can be used in a WHERE clause.
  - `AND` and `OR` are special operators that you can use with WHERE to filter the query on two or more conditions.
  - `ORDER BY` lets you sort the results of the query in either ascending or descending order.
  - `LIMIT` lets you specify the maximum number of rows that the query will return. This is especially important in large tables that have thousands or even millions of rows.
  
Example:
```sql
# --- Get the name and imdb_rating column.
SELECT name, imdb_rating  # (use * to select all columns)
FROM movies;

# --- Get all the distinct entries in the genre column.
SELECT DISTINCT genre 
FROM movies;

# --- Get all movies where imdb rating is greater than 8.
SELECT * 
FROM movies 
WHERE imdb_rating > 8;

# --- Get all movies where the name Starts with Se, ends with en and have a wildcard symbol in between, i.e. Seven and Se7en.
SELECT * 
FROM movies 
WHERE name 
LIKE 'Se_en';

# --- Get all movies that have man inside the name.
SELECT * 
FROM movies 
WHERE name 
LIKE '%man%';

% --- Get all movies with name that starts with a letter between A and J.
SELECT * 
FROM movies 
WHERE name 
BETWEEN 'A' AND 'J';

# --- Get all movies that are produced between 1990 and 2000 AND are of the genre comedy.
SELECT * 
FROM movies 
WHERE year
BETWEEN 1990 AND 2000 
AND genre = 'comedy';

# --- Get all movies that are either produced before 1980 or are a comedy.
SELECT * 
FROM movies 
WHERE genre = 'comedy' 
OR year < 1980;

# --- Get all movies sorted by descending imdb rating.
SELECT * 
FROM movies 
ORDER BY imdb_rating DESC;  # or ASC for ascending

# --- Get the three lowest rated movies.
SELECT * 
FROM movies
ORDER BY imdb_rating ASC 
LIMIT 3;
```
    
## Aggregate Functions
- Aggregate functions combine multiple rows together to form a single value of more meaningful information.
  - `COUNT()` takes the name of a column(s) as an argument and counts the number of rows where the value(s) is not `NULL`. Pass `*` as an argument if all rows should be counted.
  - `GROUP BY` is a clause that is only used with aggregate functions. It is used in collaboration with the `SELECT` statement to arrange identical data one or more columns into groups.
  - `SUM()` takes the column name as an argument and returns the sum of all the values in that column.
  - `MAX()` and `MIN()` takes the column name as an argument and returns the largest or smallest value in that column respectively.
  - `AVG()` takes a column name as an argument and returns the average value for that column.
  - `ROUND()` takes a column name and an integer as arguments. It rounds the values in the column to the number of decimal places specified by the integer.

Example:
```sql
SELECT COUNT(*) 
FROM fake_apps;

SELECT COUNT(*) 
FROM fake_apps 
WHERE price = 0;

SELECT price, COUNT(*) 
FROM fake_apps
GROUP BY price;

SELECT price, COUNT(*) 
FROM fake_apps 
WHERE downloads > 20000 
GROUP BY price;

SELECT SUM(downloads) 
FROM fake_apps;

SELECT category, SUM(downloads) 
FROM fake_apps 
GROUP BY category;

SELECT MAX(downloads) 
FROM fake_apps;

SELECT name, category, MAX(downloads) 
FROM fake_apps 
GROUP BY category;

SELECT MIN(downloads) 
FROM fake_apps;

SELECT name, category, MIN(downloads) 
FROM fake_apps 
GROUP BY category;

SELECT AVG(downloads) 
FROM fake_apps;

SELECT price, ROUND(AVG(downloads), 2) 
FROM fake_apps 
GROUP BY price;
```
## Multiple Tables


AS is a keyword in SQL that allows you to rename a column or table in the result set using an alias.
- A *primary key* serves as a unique identifier for each row or record in a given table. A table can not have more than one primary key column. By specifying that the id column is the `PRIMARY KEY`, SQL makes sure that the values in this column is unique and that none of the values in this column are `NULL`.
    - E.g. `CREATE TABLE artists(id INTEGER PRIMARY KEY, name TEXT);`
- A *foreign key* is a column that contains the primary key to another table in the database. We use foreign keys and primary keys to connect rows in two different tables. One table's foreign key holds the value of another table's primary key. Unlike primary keys, foreign keys do not need to be unique and can be `NULL`.
- One way to query multiple tables is to write a SELECT statement with multiple table names separated by a comma, also known as a *cross join*.
  - E.g. `SELECT table_name.column_name, table2_name.column2_name` FROM table_name, table2_name;
- In SQL, *joins* are used to combine data from multiple tables. 
- `INNER JOIN` will combine rows from different tables if the join condition is true. 
  - E.g. `SELECT * FROM albums JOIN artists ON albums.artist_id = artists.id;`
- `LEFT OUTER JOIN` will return every row in the left table, and if the join condition is not met, `NULL` values are used to fill in the columns from the right table.
  - E.g. `SELECT * FROM albums LEFT JOIN artists ON albums.artist_id = artists.id;`
- `AS` is a keyword in SQL that allows you to rename a column or table in the result set using an alias. NB: the columns have not been renamed in either table. The aliases only appear in the result set.
  - E.g. `SELECT albums.name AS 'Album', albums.year, artists.name AS 'Artist' FROM albums JOIN artists ON albums.artist_id = artists.id WHERE albums.year > 1980;`
  
  
  
