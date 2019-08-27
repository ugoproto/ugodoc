# Using the code

Seven different ways you can return data from two relational tables; excluding cross joins and self referencing joins:

1. `INNER JOIN`
2. `LEFT JOIN`
3. `RIGHT JOIN`
4. `OUTER JOIN`
5. `LEFT JOIN` excluding `INNER JOIN`
6. `RIGHT JOIN` excluding `INNER JOIN`
7. `OUTER JOIN` excluding `INNER JOIN`

![Joins](img/introduction_to_sql_joins/Visual_SQL_JOINS_V2.png)

For the sake of this article, 5, 6, and 7 are `LEFT EXCLUDING JOIN`, `RIGHT` Excluding `JOIN`, and `OUTER` Excluding `JOIN`, respectively. Some may argue that 5, 6, and 7 are not really joining the two tables, but for simplicity, let's refer to these as joins because you use a SQL join in each of these queries (but exclude some records with a `WHERE` clause).
 
# `INNER JOIN`

![Joins](img/introduction_to_sql_joins/INNER_JOIN.png)

This is the simplest, most understood join and is the most common. This query will return all of the records in the left table (`Table_A`) that have a matching record in the right table (`Table_B`). This join is written as follows:

```sql
SELECT <select_list> 
FROM Table_A A
INNER JOIN Table_B B
ON A.Key = B.Key
```

# `LEFT JOIN`

![Joins](img/introduction_to_sql_joins/LEFT_JOIN.png)

This query will return all of the records in the left table (`Table_A`) regardless if any of those records have a match in the right table (`Table_B`). It will also return any matching records from the right table. This join is written as follows:

```sql
SELECT <select_list>
FROM Table_A A
LEFT JOIN Table_B B
ON A.Key = B.Key
```

# `RIGHT JOIN`

![Joins](img/introduction_to_sql_joins/RIGHT_JOIN.png)

This query will return all of the records in the right table (`Table_B`) regardless if any of those records have a match in the left table (`Table_A`). It will also return any matching records from the left table. This join is written as follows:

```sql
SELECT <select_list>
FROM Table_A A
RIGHT JOIN Table_B B
ON A.Key = B.Key
```

# `OUTER JOIN`

![Joins](img/introduction_to_sql_joins/FULL_OUTER_JOIN.png)

This Join can also be referred to as a `FULL OUTER JOIN` or a `FULL JOIN`. This query will return all of the records from both tables, joining records from the left table (`Table_A`) that match records from the right table (`Table_B`). This join is written as follows:

```sql
SELECT <select_list>
FROM Table_A A
FULL OUTER JOIN Table_B B
ON A.Key = B.Key
```
 
# `LEFT` Excluding `JOIN`

![Joins](img/introduction_to_sql_joins/LEFT_EXCLUDING_JOIN.png)

This query will return all of the records in the left table (`Table_A`) that do not match any records in the right table (`Table_B`). This join is written as follows:

```sql
SELECT <select_list> 
FROM Table_A A
LEFT JOIN Table_B B
ON A.Key = B.Key
WHERE B.Key IS NULL
```

# `RIGHT` Excluding `JOIN`

![Joins](img/introduction_to_sql_joins/RIGHT_EXCLUDING_JOIN.png)

This query will return all of the records in the right table (`Table_B`) that do not match any records in the left table (`Table_A`). This join is written as follows:

```sql
SELECT <select_list>
FROM Table_A A
RIGHT JOIN Table_B B
ON A.Key = B.Key
WHERE A.Key IS NULL
```
 
# `OUTER` Excluding `JOIN`

![Joins](img/introduction_to_sql_joins/OUTER_EXCLUDING_JOIN.png)

This query will return all of the records in the left table (`Table_A`) and all of the records in the right table (`Table_B`) that do not match. I have yet to have a need for using this type of join, but all of the others, I use quite frequently. This join is written as follows:

```sql
SELECT <select_list>
FROM Table_A A
FULL OUTER JOIN Table_B B
ON A.Key = B.Key
WHERE A.Key IS NULL OR B.Key IS NULL
```

# Examples

Suppose we have two tables, `TABLE_A` and `TABLE_B`. The data in these tables are shown below:

```sql
TABLE_A
  PK Value
---- ----------
   1 FOX
   2 COP
   3 TAXI
   6 WASHINGTON
   7 DELL
   5 ARIZONA
   4 LINCOLN
  10 LUCENT

TABLE_B
  PK Value
---- ----------
   1 TROT
   2 CAR
   3 CAB
   6 MONUMENT
   7 PC
   8 MICROSOFT
   9 APPLE
  11 SCOTCH
```

The results of the seven joins are shown below:

**`INNER JOIN`**

```sql
--INNER JOIN
SELECT A.PK AS A_PK, A.Value AS A_Value,
       B.Value AS B_Value, B.PK AS B_PK
FROM Table_A A
INNER JOIN Table_B B
ON A.PK = B.PK
```

```sql
A_PK A_Value    B_Value    B_PK
---- ---------- ---------- ----
   1 FOX        TROT          1
   2 COP        CAR           2
   3 TAXI       CAB           3
   6 WASHINGTON MONUMENT      6
   7 DELL       PC            7

(5 row(s) affected)
```

**`LEFT JOIN`**

```sql
--LEFT JOIN
SELECT A.PK AS A_PK, A.Value AS A_Value,
B.Value AS B_Value, B.PK AS B_PK
FROM Table_A A
LEFT JOIN Table_B B
ON A.PK = B.PK
```

```sql
A_PK A_Value    B_Value    B_PK
---- ---------- ---------- ----
   1 FOX        TROT          1
   2 COP        CAR           2
   3 TAXI       CAB           3
   4 LINCOLN    NULL       NULL
   5 ARIZONA    NULL       NULL
   6 WASHINGTON MONUMENT      6
   7 DELL       PC            7
  10 LUCENT     NULL       NULL

(8 row(s) affected)
```

**`RIGHT JOIN`**

```sql
--RIGHT JOIN
SELECT A.PK AS A_PK, A.Value AS A_Value,
B.Value AS B_Value, B.PK AS B_PK
FROM Table_A A
RIGHT JOIN Table_B B
ON A.PK = B.PK
```

```sql
A_PK A_Value    B_Value    B_PK
---- ---------- ---------- ----
   1 FOX        TROT          1
   2 COP        CAR           2
   3 TAXI       CAB           3
   6 WASHINGTON MONUMENT      6
   7 DELL       PC            7
NULL NULL       MICROSOFT     8
NULL NULL       APPLE         9
NULL NULL       SCOTCH       11

(8 row(s) affected)
```
 
**`OUTER JOIN`**

```sql
--OUTER JOIN
SELECT A.PK AS A_PK, A.Value AS A_Value,
B.Value AS B_Value, B.PK AS B_PK
FROM Table_A A
FULL OUTER JOIN Table_B B
ON A.PK = B.PK
```

```sql
A_PK A_Value    B_Value    B_PK
---- ---------- ---------- ----
   1 FOX        TROT          1
   2 COP        CAR           2
   3 TAXI       CAB           3
   6 WASHINGTON MONUMENT      6
   7 DELL       PC            7
NULL NULL       MICROSOFT     8
NULL NULL       APPLE         9
NULL NULL       SCOTCH       11
   5 ARIZONA    NULL       NULL
   4 LINCOLN    NULL       NULL
  10 LUCENT     NULL       NULL

(11 row(s) affected)
```

**`LEFT` Excluding `JOIN`**

```sql
--LEFT EXCLUDING JOIN
SELECT A.PK AS A_PK, A.Value AS A_Value,
B.Value AS B_Value, B.PK AS B_PK
FROM Table_A A
LEFT JOIN Table_B B
ON A.PK = B.PK
WHERE B.PK IS NULL
```

```sql
A_PK A_Value    B_Value    B_PK
---- ---------- ---------- ----
   4 LINCOLN    NULL       NULL
   5 ARIZONA    NULL       NULL
  10 LUCENT     NULL       NULL
(3 row(s) affected)
```

**`RIGHT` Excluding `JOIN`**

```sql
-RIGHT EXCLUDING JOIN
SELECT A.PK AS A_PK, A.Value AS A_Value,
B.Value AS B_Value, B.PK AS B_PK
FROM Table_A A
RIGHT JOIN Table_B B
ON A.PK = B.PK
WHERE A.PK IS NULL
```

```sql
A_PK A_Value    B_Value    B_PK
---- ---------- ---------- ----
NULL NULL       MICROSOFT     8
NULL NULL       APPLE         9
NULL NULL       SCOTCH       11

(3 row(s) affected)
```

**`OUTER` Excluding `JOIN`**

```sql
--OUTER EXCLUDING JOIN
SELECT A.PK AS A_PK, A.Value AS A_Value,
B.Value AS B_Value, B.PK AS B_PK
FROM Table_A A
FULL OUTER JOIN Table_B B
ON A.PK = B.PK
WHERE A.PK IS NULL
OR B.PK IS NULL
```

```sql
A_PK A_Value    B_Value    B_PK
---- ---------- ---------- ----
NULL NULL       MICROSOFT     8
NULL NULL       APPLE         9
NULL NULL       SCOTCH       11
   5 ARIZONA    NULL       NULL
   4 LINCOLN    NULL       NULL
  10 LUCENT     NULL       NULL

(6 row(s) affected)
```

# Conclusion

Note on the `OUTER JOIN` that the inner joined records are returned first, followed by the right joined records, and then finally the left joined records (at least, that's how my Microsoft SQL Server did it; this, of course, is without using any `ORDER BY` statement).

![Joins](Visual_introduction_to_sql_joins_V2)
