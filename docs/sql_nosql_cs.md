# SQL

- [SQL](pdf/zt_sql_cheat_sheet.pdf). PDF. [See the notes below](#sql-notes).

<center>
![](img/sql_nosql/zt_sql_cheat_sheet.png)
</center>

- [SQL](pdf/SQL-Cheatsheet-2.pdf). PDF.

<center>
![](img/sql_nosql/SQL-Cheatsheet-2.png)
</center>

# SQL notes

## Basic Queries

```sql
SELECT col1, col2, col3, ... FROM table1;
```

- Commands are not case-sensitive: `SELECT` or `select`;
- `;` is not required;
- Dividing an integer by an integer gives an integer; use floats with decimals.

## Add conditions

```sql
SELECT col1 FROM table1
WHERE (col4 = "A") AND (col5 = "B" OR col6 = "C");
```

```sql
SELECT col1 FROM table1
WHERE (col4 BETWEEN 10 AND 20);
```

  - `< > = <> <= >= AND OR`.

## Filter out missing values (or non-missing values)

```sql
SELECT col1 FROM table1
WHERE col4 IS NULL;
```

```sql
SELECT col1 FROM table1
WHERE col4 IS NOT NULL;
```

## Set limits

```sql
SELECT col1 FROM table1
WHERE (col4 BETWEEN 10 AND 20)
LIMIT 3;
```

- `BETWEEN` is inclusive (like `<=` and `>=`);

## Find patterns

```sql
SELECT col1 FROM table1
WHERE col4 LIKE 'a%';
```

- regex patterns like `'a%'` for "begins with a", `"%B"` for "ends with capital B";
- `%` is a joker.

```sql
SELECT col1 FROM table1
WHERE col4 IN ('Germany', "France", 'UK');
```

- `IN` subgroups, limited to a set.

## Command hierarchy

```sql
SELECT col1, col2, col3, ... FROM table1
WHERE col4 = 1 AND col5 = 2
LIMIT 3
GROUP by ...
HAVING count(*) > 1
ORDER BY col2, col3 DESC;
```

- `DESC` or ascending by default.

## Aggregate (two ways)

Opening aggregation:

```sql
SELECT COUNT(col1) FROM table1;
```

- `COUNT` (not missing or not null values), `SUM`, `AVG`, `MIN`, `MAX`.

Closing aggregation:

```sql
SELECT col1 FROM table1
HAVING count(col2) > 1;
```
- `count`, `sum`, `avg`, `min`, `max`.

## Unique values

```sql
SELECT DISTINCT col2 FROM table1;
```

```sql
SELECT COUNT(col1) COUNT(DISTINCT col2) FROM table1;
```

## Compute, transform, create new columns

```sql
SELECT col1 + col2 AS col1b FROM table1;
```

- `+ - * /`.

## Add views

```sql
CREATE VIEW view1 AS V1
SELECT col1 FROM table1;
```

- Aliases for the headers.

# SQLite

- [SQLite](pdf/richardjh_sqlite3.pdf). PDF.

<center>
![](img/sql_nosql/richardjh_sqlite3a.png)

![](img/sql_nosql/richardjh_sqlite3b.png)
</center>

# MySQL

- [MySQL](pdf/davechild_mysql.pdf). PDF.

<center>
![](img/sql_nosql/davechild_mysqla.png)

![](img/sql_nosql/davechild_mysqlb.png)
</center>

---

- [Essential MySQL](pdf/guslong_essential-mysql.pdf). PDF.

<center>
![](img/sql_nosql/guslong_essential-mysqla.png)

![](img/sql_nosql/guslong_essential-mysqlb.png)
</center>

---

- [Essential Admin for MySQL](pdf/4107-rc029-010d-essential-admin-mysql5.5_2.pdf). PDF only.

# PostgreSQL

- [PostgreSQL](pdf/tme520_postgresql.pdf). PDF.

<center>
![](img/sql_nosql/tme520_postgresqla.png)

![](img/sql_nosql/tme520_postgresqlb.png)

![](img/sql_nosql/tme520_postgresqlc.png)
</center>

---

- [PostgreSQL Interactive Terminal Commands](pdf/squixy_postgresql-interactive-terminal-commands.pdf). PDF.

<center>
![](img/sql_nosql/squixy_postgresql-interactive-terminal-commands.png)
</center>

---

- [Essential PostgreSQL](pdf/52492-rc071_postgresql_2.pdf). PDF only.

# NoSQL

- [NoSQL and Data Scalability](pdf/4154-rc105-010d-nosql.pdf). PDF only.
- [MongoDB](pdf/4176-rc171-010d-mongodb-2.pdf). PDF only.
