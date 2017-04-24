---

[TOC]

---

**Foreword**

Code snippets. From Codecademy.

---

While working with databases, we often need to transform data from one format to achieve a desired result. In SQL, this is often called data transformation or table transformation.

## 1, Subqueries

Subqueries, sometimes referred to as inner queries or nested queries, are used to transform table data by nesting one query within another query. 

Two tables: 'airports' and 'flights'.

Select ten rows from the flights table.

```sql
SELECT * FROM flights LIMIT 10;
```sql

We first create an inner query, or subquery, that finds the 'airports' with elevation greater than 2000 from the airports table. 

```sql
SELECT code FROM airports WHERE elevation > 2000;
```

Next, we take the result set of the inner query and use it to filter on the 'flights' table, to find the flight detail that meets the elevation criteria.

```sql
SELECT * FROM flights WHERE origin in (
    SELECT code FROM airports WHERE elevation > 2000);
```

Find flight information about flights where the origin elevation is less than 2000 feet.

```sql
SELECT * FROM flights WHERE origin in (
    SELECT code FROM airports WHERE elevation < 2000);
```
 
### Non-Correlated Subqueries
 
A non-correlated subquery is a subquery that can be run independently of the outer query and as we saw, can be used to complete a multi-step transformation.

Perhaps we'd like to look at a selection of flights whose origin airport is a seaplane base, designated by SEAPLANE_BASE. The facility type of an airport is located in the fac_type field of the airports table.

```sql
SELECT * FROM flights WHERE origin in (
    SELECT code FROM airports WHERE fac_type = 'SEAPLANE_BASE');
```

Using the same pattern, find flight information about flights where the Federal Aviation Administration region (faa_region) is the Southern region (ASO).

```sql
SELECT * FROM flights WHERE origin in (
    SELECT code FROM airports WHERE faa_region = 'ASO');
```
    
Perform transformations on a single table. For instance, sometimes we need to aggregate in multiple steps - like taking an average of a count.

Imagine you’d like to know how many flights there are on average, for all Fridays in a given month from the flights table. First, we’d need to calculate the number of flights per day, and then we’d need to calculate the average based on the daily flight count for each day of the week. We can do this all in one step using a subquery:

```sql
SELECT a.dep_month,
       a.dep_day_of_week,
       AVG(a.flight_count) AS average_flights
    FROM (
        SELECT dep_month,
               dep_day_of_week,
               dep_date,
               COUNT(*) AS flight_count
        FROM flights
        GROUP BY 1,2,3
        ) a
GROUP BY 1,2
ORDER BY 1,2;
```

The inner query provides the count of flights by day, and the outer query uses the inner query’s result set to compute the average by day of week of a given month.

Using a subquery, find the average total distance flown by day of week and month. Be sure to alias the outer query as average_distance and the inner query as flight_distance.

```sql
SELECT a.dep_month,
       a.dep_day_of_week,
       AVG(a.flight_distance) AS average_distance
    FROM (
        SELECT dep_month,
              dep_day_of_week,
               dep_date,
               sum(distance) AS flight_distance
        FROM flights
        GROUP BY 1,2,3
    ) a
GROUP BY 1,2
ORDER BY 1,2;
```

### Correlated Subqueries

In a correlated subquery, the subquery can not be run independently of the outer query. The order of operations is important in a correlated subquery:

    A row is processed in the outer query.
    Then, for that particular row in the outer query, the subquery is executed.

This means that for each row processed by the outer query, the subquery will also be processed for that row. In this example, we will find the list of all flights whose distance is above average for their carrier (query on a query, same table).

```sql
SELECT id
FROM flights AS f
WHERE distance > (
    SELECT AVG(distance)
    FROM flights
    WHERE carrier = f.carrier);
```
 
In the above query the inner query has to be re-executed for each flight. Correlated subqueries may appear elsewhere besides the WHERE clause, they can also appear in the SELECT.

Find the id of the flights whose distance is below average for their carrier.

```sql
SELECT id
FROM flights AS f
WHERE distance < (
    SELECT AVG(distance)
    FROM flights
    WHERE carrier = f.carrier);
```

It would also be interesting to order flights by giving them a sequence number based on time, by carrier. For instance, assuming flight_id increments with each additional flight, we could use the following query to view flights by carrier, flight id, and sequence number:

```sql
SELECT carrier, id,
    (SELECT COUNT(*)
        FROM flights f
        WHERE f.id < flights.id
        AND f.carrier=flights.carrier) + 1 
        AS flight_sequence_number
        FROM flights;
```

Using the same pattern, write a query to view flights by origin, flight id, and sequence number. Alias the sequence number column as flight_sequence_number.

```sql
SELECT origin, id,
    (SELECT COUNT(*)
    FROM flights f
    WHERE f.id < flights.id
    AND f.origin=flights.origin) + 1 
    AS flight_sequence_number
    FROM flights;
```

### What can we generalize so far?

- Subqueries are used to complete an SQL transformation by nesting one query within another query.
- A non-correlated subquery is a subquery that can be run independently of the outer query and can be used to complete a multi-step transformation.
- A correlated subquery is a subquery that cannot be run independently of the outer query. The order of operations in a correlated subquery is as follows:
	1. A row is processed in the outer query.
	1. Then, for that particular row in the outer query, the subquery is executed.
	1. Set Operations.

Unions allow us to utilize information from multiple tables in our queries. In this lesson, we’ll utilize data from an e-commerce store. Let’s explore the available data we’ll be using. 

Four tables: 'new_products', legacy_products', 'order_items' and 'order_items_historic'.

In our database, we have products tables that contain metadata about each product in the store. Select ten rows from the new_products table.

```sql
SELECT * FROM new_products LIMIT 10;
```

## Merging Tables Together

Sometimes, in order to answer certain questions based on data, we need to merge two tables together and then query the merged result. Perhaps we have two tables that contain information about products in an ecommerce store that we would like to combine. There are two ways of doing this:

- Merge the rows, called a JOIN.
- Merge the columns, called a UNION.

### UNION

We'll focus on unions here. Union combines the result of two or more SELECT statements, using the following syntax:

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

Each SELECT statement within the UNION must have the same number of columns with similar data types. The columns in each SELECT statement must be in the same order. By default, the UNION operator selects only distinct values.

Suppose we are a growing ecommerce store and recently acquired another store to diversify our offering. The product data still exists in two separate tables: a legacy_products table and a new_products table. To get the complete list of product names from both tables, we can perform the following union.

```sql
SELECT item_name FROM legacy_products
UNION 
SELECT item_name FROM new_products;
```

Select a complete list of brand names from the legacy_products and new_products tables.

```sql
SELECT brand FROM legacy_products
UNION
SELECT brand FROM new_products;
```

What if we wanted to allow duplicate values? We can do this by using the ALL keyword with UNION, with the following syntax:

```sql
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

In our ecommerce store, if we learned that we had records from historic order items in an additional table, we could use the following query to combine the tables for a complete analysis of sale price:

```sql
SELECT id, sale_price FROM order_items
UNION ALL
SELECT id, sale_price FROM order_items_historic;
```

Then we can perform an analysis on top of the combined result set, like finding the total count of order items.

```sql
SELECT count(*) FROM (
    SELECT id, sale_price FROM order_items
    UNION ALL
    SELECT id, sale_price FROM order_items_historic) as a;
```

Using the same pattern, utilize a subquery to find the average sale price over both order_items and order_items_historic tables.

```sql
SELECT id, avg(a.sale_price) FROM (
    SELECT id, sale_price FROM order_items
    UNION ALL
    SELECT id, sale_price FROM order_items_historic) AS a 
    GROUP BY 1;
```

(before running the top analysis, create an alias a with the preliminary results, run the avg(a.sale_price), and group by 1 to view separate records and not a unique aggregate record!!!)

### INTERSECT 

...is used to combine two SELECT statements, but returns rows only from the first SELECT statement that are identical to a row in the second SELECT statement. This means that it returns only common rows returned by the two SELECT statements.

```sql
SELECT column_name(s) FROM table1
INTERSECT
SELECT column_name(s) FROM table2;
```

For instance, we might want to know what brands in our newly acquired store are also in our legacy store. We can do so using the following query:

```sql
SELECT brand FROM new_products
INTERSECT
SELECT brand FROM legacy_products;
```

Select the items in the category column that are both in the newly acquired new_products table and the legacy_products table.

```sql
SELECT category FROM new_products
INTERSECT
SELECT category FROM legacy_products;
```

### EXCEPT 

...is constructed in the same way, but returns distinct rows from the first SELECT statement that aren’t output by the second SELECT statement.

```sql
SELECT column_name(s) FROM table1
EXCEPT
SELECT column_name(s) FROM table2;
```

Suppose we want to see if there are any categories that are in the new_products table that aren't in the legacy_products table. We can use an EXCEPT query to perform this analysis:

```sql
SELECT category FROM new_products
EXCEPT
SELECT category FROM legacy_products;
```

Conversely, select the items in the category column that are in the legacy_products table and not in the new_products table.

```sql
SELECT category FROM legacy_products
EXCEPT
SELECT category FROM new_products;
```

### What can we generalize so far?

- The UNION clause allows us to utilize information from multiple tables in our queries.
- The UNION ALL clause allows us to utilize information from multiple tables in our queries, including duplicate values.
- INTERSECT is used to combine two SELECT statements, but returns rows only from the first SELECT statement that are identical to a row in the second SELECT statement.
- EXCEPT returns distinct rows from the first SELECT statement that aren’t output by the second SELECT statement

## 3, Conditional Aggregates

Aggregate functions compute a single result from a set of multiple input values. You can think of aggregate data as data collected from multiple rows at a time. In this lesson, we'll continue learning about aggregate functions by focusing on conditionals, sums, and combining aggregate functions.

Conditional Aggregates are aggregate functions that compute a result set based on a given set of conditions.

The count function is an aggregate function, since it aggregates data from multiple rows.

Count the number of rows in the flights table, representing the total number of flights contained in the table.

```sql
SELECT COUNT(*) FROM flights;
```

While working with databases, it's common to have empty or unknown "cells" in data tables.

What do we do when we need to test whether a value is or is not null? We use the special keywords IS NULL or IS NOT NULL in the WHERE clause (= NULL does not work).

Count the number of rows from the flights table, where arr_time is not null and the destination is ATL.

```sql
SELECT COUNT(*) FROM flights WHERE arr_time IS NOT NULL AND destination = "ATL";
```

Almost every programming language has a way to represent "if, then, else", or conditional logic. In SQL, we represent this logic with the CASE statement, as follows:

```sql
SELECT
    CASE
        WHEN elevation < 500 THEN 'Low'
        WHEN elevation BETWEEN 500 AND 1999 THEN 'Medium'
        WHEN elevation >= 2000 THEN 'High'
        ELSE 'Unknown'
    END AS elevation_tier, 
    COUNT(*)
FROM airports
GROUP BY 1;
```

In the above statement, END is required to terminate the statement, but ELSE is optional. If ELSE is not included, the result will be NULL. Also notice the shorthand method of referencing columns to use in GROUP BY, so we don't have to rewrite the entire Case Statement.

Modify the case statement's such that when the elevation is less than 250, the elevation_tier column returns 'Low', when between 250 and 1749 it returns 'Medium', and when greater than or equal to 1750 it returns 'High'.

Be sure to alias the conditional statement as elevation_tier, in your query.

```sql
SELECT
    CASE
        WHEN elevation < 250 THEN 'Low'
        WHEN elevation BETWEEN 250 AND 1749 THEN 'Medium'
        WHEN elevation >= 1750 THEN 'High'
        ELSE 'Unknown'
    END AS elevation_tier, 
    COUNT(*)
FROM airports
GROUP BY 1;
```

Sometimes you want to look at an entire result set, but want to implement conditions on certain aggregates.

For instance, maybe you want to identify the total amount of airports as well as the total amount of airports with high elevation in the same result set. We can accomplish this by putting a CASE WHEN statement in the aggregate.

```sql
SELECT state, 
    COUNT(CASE WHEN elevation >= 2000 THEN 1 ELSE NULL END) as count_high_elevation_aiports 
FROM airports 
GROUP BY state;
```

Using the same pattern, write a query to count the number of low elevation airports by state where low elevation is defined as less than 1000 ft. Be sure to alias the counted airports as count_low_elevation_airports.

```sql
SELECT state, 
    COUNT(CASE WHEN elevation < 1000 THEN 1 ELSE NULL END) as count_low_elevation_aiports 
FROM airports 
GROUP BY state;
```

We can do that same thing for other aggregates like SUM(). For instance, if we wanted to sum the total flight distance and compare that to the sum of flight distance from a particular airline (in this case, United Airlines) by origin airport, we could run the following query:
sum(distance) for all carriers (total_flight_distance)
sum(distance) for UA only (others are turned to 0) (total_united_flight_distance).

```sql
SELECT origin, sum(distance) as total_flight_distance, sum(CASE WHEN carrier = 'UA' THEN distance ELSE 0 END) as total_united_flight_distance 
FROM flights 
GROUP BY origin;
```

Using the same pattern, find both the total flight distance as and flight distance by origin for Delta (carrier = 'DL').

Alias the flight distance as total_flight_distance and the and flight distance by origin as total_delta_flight_distance.

```sql
SELECT origin, sum(distance) as total_flight_distance, sum(CASE WHEN carrier = 'DL' THEN distance ELSE 0 END) as total_delta_flight_distance 
FROM flights 
GROUP BY origin;
```

Using the same pattern, find the percentage of flights from Delta by origin (carrier = 'DL'):

```sql
SELECT origin, 100.0*(sum(CASE WHEN carrier = 'DL' THEN distance ELSE 0 END)/sum(distance)) as percentage_flight_distance_from_delta FROM flights 
GROUP BY origin;
```

Find the percentage of high elevation airports (elevation >= 2000) by state from the airports table. In the query, alias the percentage column as percentage_high_elevation_airports.
(sum of '1') / count(*) and not (count of '1') / count(*):

```sql
SELECT state, 100.0 * sum(CASE WHEN elevation >= 2000 THEN 1 ELSE 0 END) / count(*)  as percentage_high_elevation_airports FROM airports GROUP BY state;
```

### What can we generalize so far?

- Conditional Aggregates are aggregate functions the compute a result set based on a given set of conditions.
- NULL can be used to denote an empty field value
- CASE statements allow for custom classification of data
- CASE statements can be used inside aggregates (like SUM() and COUNT()) to provide filtered measures

## 4, Date, Number, and String Functions

Oftentimes, data in columns of tables is not in the exact format we need to complete our desired analysis. We may need to extract a date from a full timestamp, manipulate a number, or combine first and last name columns to create a full name.

In this lesson, we'll be learning about some of SQL's built-in functions for transforming dates, numbers and strings. We'll be using database of bakeries in this lesson.

It is important to note that date, number, and string functions are highly database dependent. Here, we focus on built-in functions in the SQLite database management system.

Select ten rows from the bakeries table:

```sql
SELECT * FROM bakeries LIMIT 10;
```

We'll begin with dates. Dates are often written in the following format

1. Date: YYYY-MM-DD
1. Datetime or Timestamp: YYYY-MM-DD hh:mm:ss

We can use SQL's date functions to transform data into a desired format. Since date functions can be database specific, verify the functions that exist on your relational database management system. For example, this statement:

```sql
SELECT DATETIME(manufacture_time) FROM baked_goods;
```

Using the datetime function, select the date and time of all deliveries in the baked_goods table using the column delivery_time.

```sql
SELECT DATETIME(delivery_time) FROM baked_goods;
```

Now let's assume that we have a column in our baked_goods table named manufacture_time in the format YYYY-MM-DD hh:mm:ss. We'd like to know the number of baked_goods manufactured by day, and not by second. We can use the DATE() function to easily convert timestamps to dates and complete the following query:

```sql
SELECT DATE(manufacture_time), count(*) as count_baked_goods
FROM baked_goods
GROUP BY DATE(manufacture_time);
```

Similarly, we can query the time with:

```sql
SELECT TIME(manufacture_time), count(*) as count_baked_goods
FROM baked_goods
GROUP BY TIME(manufacture_time);
```

Find the number of baked goods by date of delivery. Be sure to alias the total count of baked goods as count_baked_goods.

```sql
SELECT DATE(delivery_time), count(*) as count_baked_goods FROM baked_goods GROUP BY DATE(delivery_time);
```

Given a datepart and a column of date or timestamp data type, we can increment date or timestamp values by a specified interval. For example, in SQLite, the statement:

```sql
DATETIME(time1, '+3 hours', '40 minutes', '2 days');
```

Would return a time 3 hours, 20 minutes, and 2 days after time1.

Imagine that each dessert in our baked_goods table is inspected 2 hours, 30 minutes, and 1 day after the manufacture time. To derive the inspection date for each baked good, we can use the following query:

```sql
SELECT DATETIME(manufacture_time, '+2 hours', '30 minutes', '1 day') as inspection_time
FROM baked_goods;
```

Each of the baked goods is packaged by Baker's Market exactly five hours, twenty minutes, and two days after the delivery (designated by delivery_time). Create a query returning all the packaging times for the goods in the baked_goods table. Be sure to alias the package time column as package_time.

```sql
SELECT DATETIME(delivery_time, '+5 hours', '20 minutes', '2 days') as package_time
FROM baked_goods;
```

Numeric functions can be used to transform numbers. Some common SQLite mathematical functions are included below that take numeric data types as inputs:

- SELECT (number1 + number2);: Returns the sum of two numbers. Similar, SQL can be used for subtraction, multiplication, and division.
- SELECT CAST(number1 AS REAL) / number3;: Returns the result as a real number by casting one of the values as a real number, rather than an integer.
- SELECT ROUND(number, precision);: Returns the numeric value rounded off to the next value specified.

In our baked_goods table, we have information about cost designated by ingredients_cost. For accounting purposes, we'd like to make sure that each ingredient cost is rounded to four decimal places rather than two, to account for currency fluctuations.

```sql
SELECT ROUND(ingredients_cost, 4) as rounded_cost
FROM baked_goods;
```

Find the bakery's distance from the market rounded to two decimal places. Be sure to alias the column as distance_from_market.

```sql
SELECT ROUND(distance, 2) as distance_from_market
FROM bakeries;
```

A couple more useful numeric SQL functions are included below: MAX and MIN. MAX(n1,n2,n3,...): returns the greatest value in the set of the input numeric expressions MIN(n1,n2,n3,...): returns the least value in the set of the input numeric expressions

In our baked_goods table, in addition to the numeric ingredients_cost we have information about the packaging cost located in the packaging_cost column. We can use the MAX function to determine the overall greatest value of cost for each item using the following query:

```sql
SELECT id, MAX(ingredients_cost, packaging_cost)
FROM baked_goods;
```

We also have information about cook time designated as cook_time and cool down time designated as cool_down_time in the baked_goods table. Find the greatest time value for each item in the table.

```sql
SELECT id, MAX(cook_time, cool_down_time)
FROM baked_goods;
```

Find the least time value for each item in the table.

```sql
SELECT id, MIN(cook_time, cool_down_time)
FROM baked_goods;
```

String manipulation can be useful to derive information from columns. We'll cover a couple of the common string functions here.

A common use case for string manipulation in SQL is concatenation of strings. In SQLite, this is written as:

```sql
SELECT string1 || ' ' || string2;
```

For example, the bakeries table contains both city and state columns. In order to create a route for these columns, we use the || function to concatenate them as in the following query:

```sql
SELECT city || ' ' || state as location
FROM bakeries;
```

String functions are again, very database specific, and it is best practice to consult documentation before proceeding. 

Combine the first_name and last_name columns from the bakeries table as the full_name to identify the owners of the bakeries. Be sure to add a space between the names in the full_name as shown in the example.

```sql
SELECT first_name || ' ' || last_name as full_name FROM bakeries;
```

Another useful string function in SQL is REPLACE():

```sql
REPLACE(string,from_string,to_string)
```
The function returns the string string with all occurrences of the string from_string replaced by the string to_string. For example in baked_goods, there is a column named ingredients. The ingredients strings are formatted with underscores, such as baking_soda and vanilla_extract. To make these values more readable, we might like to replace the underscores with spaces. We can do so by using the following query:

```sql
SELECT id, REPLACE(ingredients,'_',' ') as item_ingredients
from baked_goods;
```

Any time enriched_flour appears in the ingredients list, we’d like to replace it with just flour. Apply this transformation and also be sure to remove the underscore in enriched_flour.

```sql
SELECT REPLACE(ingredients,'enriched_',' ') as item_ingredients
FROM baked_goods;
```

### What can we generalize so far?

- Date Functions:
	- DATETIME; Returns the date and time of the column specified. This can be modified to return only the date or only the time.
	- DATETIME(time1, +X hours, Y minutes, Z days): Increments the specificed column by a given number of hours, minutes, or days.
- Numeric Functions:
	- (number1 + number2);: Returns the sum of two numbers, or other mathematical operations, accordingly.
	- CAST(number1 AS REAL) / number2;: Returns the result as a real number by casting one of numeric inputs as a real number
	- ROUND(number, precision);: Returns the numeric value rounded off to the next value specified.
- String Functions:
	- 'string1' || ' ' || 'string2';: Concatenates string1 and string 2, with a space between.
	- REPLACE(string,from_string,to_string): Returns the string with all occurrences of the string from_string replaced by the string to_string.