<!--
---

[TOC]
-->
---

**Foreword**

Code Snippets. From Codecademy.

---

## Specifying Comments

- Line comment. This is indicated by two negative signs (eg. `--`). The remainder of the text on the line is the comment.
- Block comment. The start of the block comment is indicated by `/*`, the end of the comment by the same string. A block comment can cover text in part of a line, or can span multiple lines.
- `Rem` or `@`. For Oracle, a line starting with either `REM` or `@` is a comment line.

## Manipulation

SQL, for Structured Query Language, is a programming language designed to manage data stored in relational databases. SQL operates through simple, declarative statements. This keeps data accurate and secure, and helps maintain the integrity of databases, regardless of size.

The SQL language is widely used today across web frameworks and database applications. Knowing SQL gives you the freedom to explore your data, and the power to make better decisions. By learning SQL, you will also learn concepts that apply to nearly every data storage system.

The statements covered in this course, use SQLite Relational Database Management System (RDBMS). You can learn more about RDBMS's here. You can also access a glossary of all the SQL commands taught in this course here.

```sql
--Show, create, use database

SHOW databases;
CREATE DATABASE dbname;
SHOW databases;
USE dbname;
```

```sql
--Show tables

SHOW tables;
```

```sql
--Create the table:

CREATE TABLE table_name (
    column_1 data_type, 
    column_2 data_type, 
    column_3 data_type
  );
```

```sql 
CREATE TABLE celebs (id INTEGER, name TEXT, age INTEGER);
```

```sql
--Add a row:

INSERT INTO celebs (id,name,age) VALUES (1,"Justin Bieber",21);
```

```sql
--View:

SELECT * From celebs;
```

```sql
--Insert more rows:

INSERT INTO celebs (id,name,age) VALUES (2,"Beyonce Knowles",33);
INSERT INTO celebs (id,name,age) VALUES (3,"Jeremy Lin",26);
INSERT INTO celebs (id,name,age) VALUES (4,"Taylor Swift",26);
```

```sql
--View:

SELECT name FROM celebs;
```

```sql
--Edit a row:

UPDATE celebs SET age = 22 WHERE id = 1;
```

```sql
--View:

SELECT * FROM celebs;
```

```sql
--Add a new column:

ALTER TABLE celebs ADD COLUMN twitter_handle TEXT;
```

```sql
--View:

SELECT * FROM celebs;
```

```sql
--Update the table:

UPDATE celebs SET twitter_handle = '@taylorswift13' WHERE id = 4;
```

```sql
--View:

SELECT * FROM celebs;
```

```sql
--Delete rows. NULL for missing or unknown data:

DELETE FROM celebs WHERE twitter_handle IS NULL;
```

```sql
--View:

SELECT * FROM celebs;
```

### Project Create Table

In this project you will create your own friends table and add and delete data from it.

The instructions provided are a general guideline, but feel free to add more columns, insert more data, or create more tables.

Notes: plan a project by drawing an ULM schema.

```sql
CREATE TABLE friends (id INTEGER, name TEXT, birthday DATE);

SELECT * FROM friends;

DROP tables friends;

CREATE TABLE friends (id INTEGER, name TEXT, birthday DATE);

SHOW tables;

INSERT INTO friends (id, name, birthday) VALUES (1,"Jane Doe",'1993-05-19');
INSERT INTO friends (id, name, birthday) VALUES (2,"Jade Donot",'1995-06-12');
INSERT INTO friends (id, name, birthday) VALUES (3,"Jack Doom",'1990-10-01');
INSERT INTO friends (id, name, birthday) VALUES (4,"John Doe",'1988-12-09');

UPDATE friends SET name = "Jane Smith" WHERE id = 1; 

ALTER TABLE friends ADD COLUMN email TEXT;

UPDATE friends SET email = "jdoe@example.com" WHERE id = 1;
UPDATE friends SET email = "jade@example.com" WHERE id = 2;
UPDATE friends SET email = "doom@example.com" WHERE id = 3;
UPDATE friends SET email = "johndoe@example.com" WHERE id = 4;

DELETE FROM friends WHERE id = 1;
```

## Queries

One of the core purposes of the SQL language is to retrieve information stored in a database. This is commonly referred to as querying. Queries allow us to communicate with the database by asking questions and having the result set return data relevant to the question. In this lesson, you will be querying a database with one table named movies. Let's get started.

```sql
--Find rows:

SELECT name, imdb_rating FROM movies;
```

```sql
--Find rows. SELECT DISTINCT for unique values in the result set. It filters out all duplicate values:

SELECT DISTINCT genre FROM movies;
```

```sql
--Find rows with WHERE:

SELECT * FROM movies WHERE imdb_rating > 8;
```

Clauses:

- `=`, equals.
- `!=`, not equals.
- `>`, greater than.
- `<`, less than.
- `>=`, greater than or equal to.
- `<=`, less than or equal to.

```sql
--Find rows with LIKE. Se_en represents a pattern with a wildcard character. The _ means you can substitute any individual character here without breaking the pattern. The names Seven and Se7en both match this pattern:

SELECT * FROM movies WHERE name LIKE 'Se_en';
```

```sql
--Find rows with LIKE. % is another wildcard character that can be used with LIKE. % is a wildcard character that matches zero or more missing letters in the pattern. A% matches all movies with names that begin with "A". %a matches all movies that end with "a":

SELECT * FROM movies WHERE name LIKE 'a%';
SELECT * FROM movies WHERE name LIKE '%man%';
```

```sql
--Find rows with BETWEEN. The values can be numbers, text or dates. Names that begin with letters "A" up to but not including "J". Years between 1990 up to and including 2000:

SELECT * FROM movies WHERE name BETWEEN 'A' AND 'J';
SELECT * FROM movies WHERE year BETWEEN 1990 AND 2000;
```

```sql
--Find rows with BETWEEN, AND:

SELECT * FROM movies WHERE year BETWEEN 1990 AND 2000 AND genre = 'comedy';
```

```sql
--Find rows with BETWEEN, OR:

SELECT * FROM movies WHERE genre = 'comedy' OR year < 1980;
```

```sql
--Find rows with BETWEEN, ORDERED BY, DESC, ASC:

SELECT * FROM movies ORDER BY imdb_rating DESC;
```

```sql
--Find rows, BETWEEN, ORDERED BY, ASC. LIMIT is a clause that lets you specify the maximum number of rows the result set will have:

SELECT * FROM movies ORDER BY imdb_rating ASC LIMIT 3;
```

### Project Writing Queries

In this project you will write queries to retrieve information from the movies table.

The instructions provided are a general guideline, but feel free to experiment writing your own queries.

```sql
--Return all of the unique years in the movies table.

SELECT DISTINCT year FROM movies;

--Return all of the unique years in the movies table sorted from oldest to newest.

SELECT DISTINCT year FROM movies ORDER BY year ASC;

--Return all movies that are dramas.

SELECT * FROM movies WHERE genre = "drama";

--Return all of the movies with names that contain "bride".

SELECT * FROM movies WHERE name LIKE '%Br%';

--Return all of the movies that were made between 2000 and 2015.

SELECT * FROM movies WHERE year >= 2000 AND year <= 2015;

--Return all of the movies that were made in 1995 or have an IMDb rating of 9.

SELECT * FROM movies WHERE year = 1995 OR imdb_rating = 9;

--Return the name and IMDb rating of every movie made after 2009 in alphabetical order.

SELECT name, imdb_rating FROM movies WHERE year > 2009 ORDER BY name ASC;

--Return 3 movies with an IMDb rating of 7.

SELECT * FROM movies WHERE imdb_rating = 7 LIMIT 3;

--Return 10 movies with an IMDb rating greater than 6, are comedies, were made after 1995, and sorted by IMDb rating from highest to lowest. (Hint: you can use AND more than once in a statement).

SELECT * FROM movies WHERE imdb_rating > 6 AND genre = 'comedy' AND year > 1995 ORDER BY imdb_rating ASC LIMIT 10;

--Return all movies named 'Cast Away'.
SELECT * FROM movies WHERE name = 'Cast Away';

--Return all movies with an IMDb rating not equal to 7.
SELECT * FROM movies WHERE imdb_rating != 7;

--Return all movies with a horror genre and an IMDb rating less than 6.
SELECT * FROM movies WHERE genre = 'horror' AND imdb_rating < 6;

--Return 10 movies with an IMDb rating greater than 8 sorted by their genre.
SELECT * FROM movies WHERE imdb_rating > 8 ORDER BY genre ASC LIMIT 10;

--Return all movies that include 'King' in the name.
SELECT * FROM movies WHERE name LIKE '%King%';

--Return all movies with names that end with the word 'Out'
SELECT * FROM movies WHERE name LIKE '%Out';

--Return all movies with names that begin with the word "The" sorted by IMDb rating from highest to lowest
SELECT * FROM movies WHERE name LIKE 'The%' ORDER BY imdb_rating DESC;

--Return all of the movies.
SELECT * FROM movies;

--Return the name and id of each movie with an id greater than 125.
SELECT name, id FROM movies WHERE id > 125;

--Return all movies with names that begin with 'X-Men'
SELECT * FROM movies WHERE name LIKE 'X-Men%';

--Return the first 10 movies sorted in reverse alphabetical order.
SELECT * FROM movies DESC LIMIT 10;

--Return the id, name, and genre of all movies that are romances.
SELECT id, name, genre FROM movies WHERE genre = 'romance';

--Return all of the Twilight movies in order from the year they were released from oldest to newest.
SELECT * FROM movies WHERE name LIKE '%Twilight%' ORDER BY year ASC;

--Return all of the movies that were released in 2012 that are comedies.
SELECT * FROM movies WHERE year = 2012 AND genre = 'comedy';
```

## Aggregate Functions

Aggregate functions compute a single result from a set of input values. For instance, when we need the sum or average of a particular column, we can use aggregate functions to quickly compute it for us. We will be learning about different aggregate functions in this lesson.

For this lesson we have given you a table named fake_apps which is made up of data for fake mobile applications.

```sql
--View:

SELECT * FROM fake_apps;
```

```sql
--Calculate the number of rows in a table. where the column is not NULL. Here, we want to count every row so we pass * as an argument:

SELECT COUNT(*) FROM fake_apps;
```

```sql
--Count * or columns):

SELECT COUNT(*) FROM fake_apps WHERE price = 0;
```

```sql
--Aggregate. GROUP BY is a clause in SQL that is only used with aggregate functions. It is used in collaboration with the SELECT statement to arrange identical data into groups. Here, our aggregate function is COUNT() and we are passing price as an argument to GROUP BY. SQL will count the total number of apps for each price in the table:

SELECT price, COUNT(*) FROM fake_apps GROUP BY price;
```

```sql
--It calculates the total number of apartments in each neighborhood in the cities table and groups them by neighborhood.

SELECT neighborhood, SUM(apartments) FROM cities GROUP BY neighborhood;
```

```sql
--Sum up, aggregate by category:

SELECT category, SUM(downloads) FROM fake_apps GROUP BY category;
```

```sql
--Find the maximum, minimum, global, categorical:
SELECT MAX(downloads) FROM fake_apps;
SELECT name, category, MAX(downloads) FROM fake_apps GROUP BY category;

SELECT MIN(downloads) FROM fake_apps;
SELECT name, category, MIN(downloads) FROM fake_apps GROUP BY category;
```

```sql
--It returns the title, genre and checkout count for the book with the most checkouts in the library_books table.

SELECT title, genre, MAX(checkouts) FROM library_books
GROUP BY genre;
```

```sql
--Find the average, or category average:

SELECT AVG(downloads) FROM fake_apps;
SELECT price, AVG(downloads) FROM fake_apps GROUP BY price;
```

```sql
--Round up to x decimal(s):

SELECT price, ROUND(AVG(downloads), 2) FROM fake_apps GROUP BY price;
```

### Project Fake Apps

In this project you will write queries with aggregate functions to retrieve information from the fake_apps table.

The instructions provided are a general guideline, but feel free to experiment writing your own queries, creating your own tables, or adding your own apps to the existing table!

```sql
--Return the total number of apps in the table fake_apps.

SELECT COUNT(*) FROM fake_apps;

--Return the name, category, and price of the app that has been downloaded the least amount of times.

SELECT name, category, price, MIN(downloads) FROM fake_apps;

--Return the total number of apps for each category.

SELECT COUNT(*) FROM fake_apps GROUP BY category;

--Return the name and category of the app that has been downloaded the most amount of times.

SELECT name, category, MAX(downloads) FROM fake_apps;

--Return the name and category of the app that has been downloaded the least amount of times.

SELECT name, category, MIN(downloads) FROM fake_apps;

--Return the average price for an app in each category.

SELECT AVG(price) FROM fake_apps GROUP BY category;

--Return the average price for an app in each category. Round the averages to two decimal places.

SELECT ROUND(AVG(price),2) FROM fake_apps GROUP BY category;

--Return the maximum price for an app.

SELECT MAX(price) FROM fake_apps;

--Return the minimum number of downloads for an app.

SELECT MIN(downloads) FROM fake_apps;

--Return the total number of downloads for apps that belong to the Games category.

SELECT MIN(downloads) FROM fake_apps WHERE category = 'Games';

--Return the total number of apps that are free.

SELECT COUNT(*) FROM fake_apps WHERE price = 0;

--Return the total number of apps that cost 14.99.

SELECT COUNT(*) FROM fake_apps WHERE price = 14.99;

--Return the sum of the total number of downloads for apps that belong to the Music category.

SELECT SUM(downloads) FROM fake_apps WHERE category = 'Music';

--Return the sum of the total number of downloads for apps that belong to the Business category.

SELECT SUM(downloads) FROM fake_apps WHERE category = 'Business';

--Return the name of each category with the total number of apps that belong to it.

SELECT name, COUNT(*) FROM fake_apps GROUP BY category;

--Return the price and average number of downloads grouped by price.

SELECT price, AVG(downloads) FROM fake_apps GROUP BY price;

--Return the price and average number of downloads grouped by price. Round the averages to the nearest integer.

SELECT ROUND(price,0), AVG(downloads) FROM fake_apps GROUP BY price;

--Return the name and category and price of the most expensive app for each category.

SELECT name, category, price, MAX(price) FROM fake_apps GROUP BY category;

--Return the total number of apps whose name begin with the letter 'A'.

SELECT COUNT(*) FROM fake_apps WHERE name LIKE 'A%';

--Return the total number of downloads for apps belonging to the Sports or Health & Fitness category.

SELECT SUM(downloads) FROM fake_apps WHERE category = 'Sports' OR category = 'Health & Fitness';
```

## Multiple Tables

Most of the time, data is distributed across multiple tables in the database. Imagine a database with two tables, artists and albums. An artist can produce many different albums, and an album is produced by an artist.

The data in these tables are related to each other. Through SQL, we can write queries that combine data from multiple tables that are related to one another. This is one of the most powerful features of relational databases.

```sql
--We have created a table named albums for you. Create a second table named artists. Using the CREATE TABLE statement we added a PRIMARY KEY to the id column. A primary key serves as a unique identifier for each row or record in a given table. The primary key is literally an id value for a record. We're going to use this value to connect artists to the albums they have produced. By specifying that the id column is the PRIMARY KEY, SQL makes sure that none of the values in this column are NULL and each value in this column is unique:

CREATE TABLE artists(id INTEGER PRIMARY KEY, name TEXT);

--View both tables:

SELECT * FROM albums;
SELECT * FROM artists;
```

```sql
--Query:

SELECT * FROM artists WHERE id = 3;
```

```sql
--A foreign key is a column that contains the primary key of another table in the database. We use foreign keys and primary keys to connect rows in two different tables. One table's foreign key holds the value of another table's primary key. Unlike primary keys, foreign keys do not need to be unique and can be NULL. Here, artist_id is a foreign key in the albums table. We can see that Michael Jackson has an id of 3 in the artists table. All of the albums by Michael Jackson also have a 3 in the artist_id column in the albums table. This is how SQL is linking data between the two tables. The relationship between the artists table and the albums table is the id value of the artists.

SELECT * FROM albums WHERE artist_id = 3;
```

```sql
--One way to query multiple tables is to write a SELECT statement with multiple table names separated by a comma. This is also known as a CROSS JOIN. Here, albums and artists are the different tables we are querying. When querying more than one table, column names need to be specified by table_name.column_name. Here, the result set includes the name and year columns from the albums table and the name column from the artists table. Unfortunately the result of this cross join is not very useful. It combines every row of the artists table with every row of the albums table. It would be more useful to only combine the rows where the album was created by the artist.

SELECT albums.name, albums.year, artists.name FROM albums, artists;
```

```sql
--In SQL, joins are used to combine rows from two or more tables. The most common type of join in SQL is an INNER JOIN. An inner join will combine rows from different tables if the join condition is true. Let's look at the syntax to see how it works. SELECT * specifies the columns our result set will have. Here, we want to include every column in both tables. FROM albums specifies the first table we are querying. JOIN artists ON specifies the type of join we are going to use as well as the name of the second table. Here, we want to do an inner join and the second table we want to query is artists. albums.artist_id = artists.id is the join condition that describes how the two tables are related to each other. Here, SQL uses the foreign key column artist_id in the albums table to match it with exactly one row in the artists table with the same value in the id column. We know it will only match one row in the artists table because id is the PRIMARY KEY of artists.

SELECT * FROM albums JOIN artists ON albums.artist_id = artists.id;
```

```sql
--OUTER JOINS (LEFT or RIGHT) also combine rows from two or more tables, but unlike inner joins, they do not require the join condition to be met. Instead, every row in the left table is returned in the result set, and if the join condition is not met, then NULL values are used to fill in the columns from the right table. The left table is simply the first table that appears in the statement. Here, the left table is albums. Likewise, the right table is the second table that appears. Here, artists is the right table.

SELECT * FROM albums LEFT JOIN artists ON albums.artist_id = artists.id;
```

```sql
--AS is a keyword in SQL that allows you to rename a column or table using an alias. The new name can be anything you want as long as you put it inside of single quotes. Here we want to rename the albums.name column as 'Album', and the artists.name column as 'Artist'. It is important to note that the columns have not been renamed in either table. The aliases only appear in the result set.

SELECT albums.name, albums.year, artists.name FROM albums JOIN artists ON albums.artist_id = artists.id WHERE albums.year > 1980;
```

```sql
SELECT albums.name AS 'Album', albums.year, artists.name AS 'Artist' FROM albums JOIN artists ON albums.artist_id = artists.id WHERE albums.year > 1980;
```

### Recap

- Primary Key is a column that serves a unique identifier for row in the table. Values in this column must be unique and cannot be `NULL`.
- Foreign Key is a column that contains the primary key to another table in the database. It is used to identify a particular row in the referenced table.
- Joins are used in SQL to combine data from multiple tables.
- `INNER JOIN` will combine rows from different tables if the join condition is true.
- `LEFT OUTER JOIN` will return every row in the left table, and if the join condition is not met, `NULL` values are used to fill in the columns from the right table.
- `AS` is a keyword in SQL that allows you to rename a column or table in the result set using an alias.

### Project Querying Tables

In this project you will practice querying multiple tables using joins.

The instructions provided are a general guideline, but feel free to experiment creating your own tables, adding data, and writing more queries.

```sql
--Create a table named tracks with an id, title, and album_id column. The id column should be the PRIMARY KEY.

CREATE TABLE tracks (id INTEGER PRIMARY KEY, title TEXT, albums_id INTEGER);

--"Smooth Criminal" is a track from Michael Jackson's "Bad" album. Add this track to the database.

INSERT INTO tracks (id,title,albums_id) VALUES (1,"Smooth Criminal", 8);

--Add more tracks to the database.
INSERT INTO tracks (id,title,albums_id) VALUES (2,"aaa", 1);
INSERT INTO tracks (id,title,albums_id) VALUES (3,"bbb", 1);
INSERT INTO tracks (id,title,albums_id) VALUES (4,"ccc", 8);
INSERT INTO tracks (id,title,albums_id) VALUES (5,"ddd", 8);
INSERT INTO tracks (id,title,albums_id) VALUES (6,"eee", 8);

--Combine the albums and tracks tables using an INNER JOIN. Order the query by album_id.

SELECT * FROM albums JOIN tracks ON albums.artist_id = tracks.id;

--Combine the albums and artists table using a LEFT OUTER JOIN. Let albums be the left table.

SELECT * FROM albums LEFT JOIN artists ON albums.artist_id = artists.id;

--Combine the albums and artists table using a LEFT OUTER JOIN. Let artists be the left table.

SELECT * FROM artists LEFT JOIN albums ON albums.artist_id = artists.id;

--Use any join you like to combine the albums and tracks table. Rename the album_id column to Albums.

SELECT * FROM albums LEFT JOIN tracks ON albums.artist_id = tracks.id;
```
