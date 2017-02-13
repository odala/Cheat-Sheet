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
  - `CHECK` is used to limit the value range that can be placed in a column.
  
Example:
```sql
# --- Creates a table with the following columns: id, title, genre, year.
CREATE TABLE movies (
    id INTEGER PRIMARY KEY, 
    title TEXT, 
    genre TEXT, 
    year INTEGER CHECK (year < 2018)
);

# --- Insert two rows into the table.
INSERT INTO movies (id, title, genre, year) # the column list can be omitted if data for all values are supplied.
VALUES (1, 'Seven', 'Action', 1995);
INSERT INTO movies (id, title, genre, year) 
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

*Some of the most common data types are:*

1. Boolean, `BOOLEAN`
2. Character, `CHAR`
3. Text string, `TEXT`
4. Exact numeric, `NUMERIC`, `DECIMAL | DEC`, `INTEGER | INT`, `SMALLINT`, `BIGINT` 
5. Approximate numeric, `FLOAT`, `REAL`, `DOUBLE PRECISION`
6. Datetime data, `DATE` (YYYY-MM-DD), `TIME` (HH:MI:SS), `TIMESTAMP` (YYYY-MM-DD HH:MI:SS)
7. Interval, used to represent periods of time, `INTERVAL`
8. Large objects, used to hold large amount of data, i.e. text or graphics file.
  - `CHARACTER LARGE OBJECT`
  - `BINARY LARGE OBJECT`
  
*ISO SQL scalar operators*: 
  - arithmetic operators (`+`, `-`, `*`, `/`),
  - `OCTET_LENGTH`, `CHAR_LENGTH`, `CAST`, `||`, `CURRENT_USER`, `SESSION_USER`, `SYSTEM_USER`, `LOWER`, `UPPER`, `TRIM`, `POSITION`, `SUBSTRING`, `CASE`,
  - `CURRENT_DATE`, `CURRENT_TIME`, `CURRENT_TIMESTAMP`, `EXTRACT`, 
  - `ABS`, `MOD`, `LN`, `EXP`, `POWER`, `SQRT`, `FLOOR`, `CEIL`.
  
## Retrieve Information from a Database by Writing Queries
  - `SELECT` is the clause you use every time you want to query information from a database.
  - `SELECT DISTINCT` specifies that the statement is going to be a query that returns unique values in the specified column(s).
  - `WHERE` is a popular command that lets you filter the results of the query based on conditions that you specify.
    - `LIKE` and `BETWEEN` are special operators that can be used in a WHERE clause. 
      - *Pattern matching*: The % character represents any sequence of zero or more characters, while the _ underscore character represents any single character. Use an escape character to represent the pattern matching character, e.g. `LIKE '15#%' ESCAPE '#'`.
    - `AND` and `OR` are special operators that you can use with WHERE to filter the query on two or more conditions.
    - `IN` (or `NOT IN`) tests wheter a data value mathes one of a list of values. 
  - `ORDER BY` lets you sort the results of the query in either ascending or descending order.
  - `LIMIT` lets you specify the maximum number of rows that the query will return. This is especially important in large tables that have thousands or even millions of rows.
  
Example:
```sql
# --- Query to look at table in undefined order.
SELECT *
FROM movies;

# --- Query to look at specified columns.
SELECT name, imdb_rating
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

# --- Get all movies that are either a sci-fi or an action movie.
SELECT * 
FROM movies 
WHERE genre IN ('sci-fi', 'action');

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
  - `GROUP BY` is a clause that is only used with aggregate functions. It is used in collaboration with the `SELECT` statement to arrange identical data from one or more columns into groups. All column names in the `SELECT` list must appear in the `GROUP BY` clause unless the name is used only in an aggregate function.
    - `HAVING` is clause that is used with `GROUP BY` to restrict the groups that appear in the final result table. The search condition always includes at least one aggregate function. Column names used in the `HAVING` clause must also appear in the `GROUP BY` list or contained within an aggregate function in the `SELECT` list.
  - `COUNT()` takes the name of a column(s) as an argument and counts the number of rows where the value(s) is not `NULL`. Use `DISTINCT` before the column name in the function argument  to eliminate duplicates. Pass `*` as an argument if all rows should be counted regardless of wheter nulls or duplicate values occur.
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

SELECT category, SUM(downloads) 
FROM fake_apps 
GROUP BY category 
HAVING SUM(dowloads) > 1000
ORDER BY SUM(downloads);

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

## Subqueries
A subquery produces a temporary table with results that can be accessed and used by the outer statement. A subquery can be used immediately following a relational operator in a `WHERE` clause, or a `HAVING` clause (it must appear on the right-hand side of a comparison). The subquery itself is always enclosed in parentheses.

The keywords `ANY` and `ALL` may be used in front of subqueries that produce a single column of numbers. If the subquery is preceded by `ALL` the condition will be true only of it is satisfied by all values produced by the subquery. If the subquery is preceded by `ANY` the condition will be true if it is satisfied by any (one or more) values produced by the subquery. If the subquery is empty, the `ALL` condition returns true, the `ANY` condition return false.

The keywords `EXISTS` and `NOT EXISTS` produce a simple true/false result. `EXISTS` is true if and only if there exists at least one row in the result returned by the subquery; it is false if the subquery retyurn an empty result table. `NOT EXISTS` is the opposite.

```sql
# --- Scalar subquery returns a single column and a single row, that is, a single value.
SELECT staffNo, Name, lName, position
FROM staff
WHERE branchNo = (SELECT branchNo
                  FROM branch
                  WHERE street = '163 Main St'
                  );
                  
SELECT staffNo, Name, lName, position, salary - (SELECT AVG(salary) FROM staff) AS salDiff
FROM staff
WHERE salary > (SELECT AVG(salary) FROM staff);

SELECT staffNo, fName, lName, position
FROM staff
WHERE EXISTS (SELECT *
              FROM branch
              WHERE staff.branchNo = branch.branchNo AND city = 'London'
              );

# --- Row subquery returns multiple columns, but only a single row. Typically used in predicates.

# --- Table subquery returns one or more columns and multiple rows. For example used as an operand for the IN predicate.
SELECT propertyNo, street, city, postcode, type, rooms, rent
FROM propertyForRent
WHERE staffNo IN (SELECT staffNo
                  FROM staff
                  WHERE branchNo = (SELECT branchNo
                                    FROM branch
                                    WHERE street = '163 Main St'
                                    )
                  );
```

## Multiple Tables

AS is a keyword in SQL that allows you to rename a column or table in the result set using an alias.
- A *primary key* serves as a unique identifier for each row or record in a given table. A table can not have more than one primary key column. By specifying that the id column is the `PRIMARY KEY`, SQL makes sure that the values in this column is unique and that none of the values in this column are `NULL`.
    - E.g. `CREATE TABLE artists(id INTEGER PRIMARY KEY, name TEXT);`
- A *foreign key* is a column that contains the primary key to another table in the database. We use foreign keys and primary keys to connect rows in two different tables. One table's foreign key holds the value of another table's primary key. Unlike primary keys, foreign keys do not need to be unique and can be `NULL`.
- One way to query multiple tables is to write a SELECT statement with multiple table names separated by a comma, also known as a *cross join*. A two-table query without a `WHERE` clause produces the Cartesian product of the two tables.
  - E.g. `SELECT tableName1.column_name, tableName2.column_name FROM tableName1, tableName2`;
  - E.g. `SELECT tableName1.column_name, tableName2.column_name FROM tableName1 CROSS JOIN tableName2`;
- In SQL, *joins* are used to combine data from multiple tables. 
- `INNER JOIN` will combine rows from different tables if the join condition is true. 
  - E.g. `SELECT * FROM artists JOIN albums ON albums.artist_id = artists.artist_id;`  # Produce a table with two identical artist_id columns.
  - E.g. `SELECT * FROM artists JOIN albums USING artist_id;`  # Produce a table with one artist_id column.
  - E.g. `SELECT * FROM artists NATURAL JOIN albums;`  # Produce a table with one artist_id column.
- `LEFT OUTER JOIN` will return every row in the left table, and if the join condition is not met, `NULL` values are used to fill in the columns from the right table. (`RIGHT OUTER JOIN` returns every row in the right table, while `FULL OUTER JOIN` return every row in both tables.)
  - E.g. `SELECT * FROM albums LEFT JOIN artists ON albums.artist_id = artists.id;`
- `AS` is a keyword in SQL that allows you to rename a column or table in the result set using an alias. NB: the columns have not been renamed in either table. The aliases only appear in the result set.
  - E.g. `SELECT albums.name AS 'Album', albums.year, artists.name AS 'Artist' FROM albums JOIN artists ON albums.artist_id = artists.id WHERE albums.year > 1980;`
  
## Combining result tables
- `UNION`
  - E.g. `(SELECT city FROM branch WHERE city IS NOT NULL) UNION (SELECT city FROM propertyForRent WHERE city IS NOT NULL);`
- `INTERSECT`
  - E.g. `(SELECT city FROM branch) INTERSECT (SELECT city FROM propertyForRent)`
- `EXCEPT`
  - E.g. `(SELECT city FROM branch) EXCEPT (SELECT city FROM propertyForRent)`
- An equivalent form would be to use * instead of `city` in the two `SELECT` statements and place `CORRESPONDING BY city` behind `UNION | INTERSECT | EXCEPT`.
  
## Integrity enhancement feature

The following constraints can be defined in the `CREATE` and `ALTER TABLE` statements:
- Required data, e.g. if the column `position` cannot be null write `position VARCHAR(10) NOT NULL`.
- Domain constraints, e.g. the sex of a member is either 'M' or 'F'. Write either  `sex CHAR NOT NULL CHECK(sex IN('M', 'F'))` or `sex SexType NOT NULL` where `CREATE DOMAIN SexType AS CHAR DEFAULT 'M' CHECK (VALUE IN ('M', 'F'));` (Domains can be dropped using the statement: ´DROP DOMAIN DomainName [RESTRICT | CASCADE]´.)
- Entity integrity, a unique nonnull value for each row. For the primary key: `PRIMARY KEY(columnName (, ...))`. For other columns: `columnName1 DATATYPE1 NOT NULL, columnName2 DATATYPE2 NOT NULL, UNIQUE(columnName1, columnName2)`.
- Referential integrity, links each row in the child table containing the foreign key to the row of the parent table containing the matching candidate key value. `FOREIGN KEY(childColumnName) REFERENCES parentTable [ON DELETE CASCADE | SET NULL | SET DEFAULT | NO ACTION]`.
- General constraints. The `CREATE ASSERTION assertionName CHECK(searchCondition)` statement is an integrity constraint that is not directly linked with a table definition. This statement is similar to the `CHECK` clause, however, when a general constraint involves more than one table, it may be preferable to use this rather than duplicate the check in each table.
  
  
## General form for creating, alterin and removing a table
```sql
CREATE TABLE TableName(
  {columnName dataType [NOT NULL] [UNIQUE] [DEFAULT defaultOption] [CHECK(searchCondition)] [, ...]}
  [PRIMARY KEY (listOfColumns),]
  {[UNIQUE (listOfColumns)][, ...]}
  {[FOREIGN KEY (listOfForeignKeyColumns) REFERENCES ParentTableName [(listOfCandidateKeyColumns)]
    [MATCH {PARTIAL | FULL}]
    [ON UPDATE referentialAction]
    [ON DELETE referentialAction]] [, ...]}
  {[CHECK(searchCondition)][,...]});
```
```sql
ALTER TABLE TableName
[ADD columnName dataType [NOT NULL] [UNIQUE]]
[DEFAULT defaultOption][CHECK(searchCondition)]
[DROP columnName [RESTRICT | CASCADE]]
[ADD [CONSTRAINT [ConstraintName]] tableConstraintDefintion]
[DROP CONSTRAINT ConstraintName [RESTRICT | CASCADE]]
[ALTER columnName SET DEFAULT defaultOption]
[ALTER columnName DROP DEFAULT];
```

```sql
DROP TABLE TableName [RESTRICT | CASCADE];
```

## General form for creating and removing a view
```sql
CREATE VIEW ViewName [(newColumnName [, ...])]
AS subselect [WITH [CASCADED | LOCAL] CHECK OPTION];

DROP VIEW ViewName [RESTRICT | CASCADE];
```

## General form of a SQL query
Each clause in a statement should begin on a new line; the beginning of each clause should line up with the begiinning of other clauses; if a clause has several parts, they should appear on a separate line and be indented under the start of the clause to show the relationship; uppercase letters are used to represent reserved words; lowercase letters are used to represent user-defined words; a vertical bar indicates a choice among alternative; curly braces indicate a required element; square brackets indicate an optional element; and an ellipsis is used to indicate optional repetition of an item zero or more times.
```sql
SELECT [DISTINCT | ALL] {* | [columnExpression [AS newName]] (, ...)}
FROM tableName [AS alias] (, ...)
[WHERE condition]
[GROUP BY columnlist] [HAVING condition]
[ORDER BY columnlist] [DESC | ASC] (, ...);
```
