# PostgreSQL

> PostgreSQL: The world's most advanced open-source relational database</br>
> [https://www.postgresql.org](https://www.postgresql.org/)

> freeCodeCamp - Learn PostgreSQL </br>
> [YouTube](https://youtu.be/qw--VYLpxG4)
</br>

## Connecting to the Database

```sql
> psql
```
`psql` is the PostgreSQL command line shell. It allows us to interact with the database from our terminal. We should see a brief response indicating that we are now in:

```sql
psql (9.5.10)
Type "help" for help.
```

List any databases:

```sql
\l
```

To leave the `psql` command-line shell we can type `\q`.

</br>

## Create a Database

First, made sure you are inside the Postgres CLI.

```sql
CREATE DATABASE database_name;
```

Once the database is created, we need to tell Postgres that we want to use it.

```sql
\c database_name;
```

Once connected successfully, we should see this output in the terminal:

```sql
You are now connected to database "test_db" as user "vagrant".
database_name=#
```

</br>

## Create a Table

```sql
-- use snake_case
CREATE TABLE famous_people (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR(50),
  last_name VARCHAR(50),
  birthdate DATE
);
```

The `psql` shell allows us to type commands over multiple lines. The semicolon `;` at the end of a given command is what makes that command execute on the PostgreSQL server.

</br>

## Insert Data into a Table

```sql
INSERT INTO famous_people (first_name, last_name, birthdate)
  VALUES ('Abraham', 'Lincoln', '1809-02-12');
INSERT INTO famous_people (first_name, last_name, birthdate)
  VALUES ('Mahatma', 'Gandhi', '1869-10-02');
INSERT INTO famous_people (first_name, last_name, birthdate)
  VALUES ('Paul', 'Rudd', '1969-04-06');
INSERT INTO famous_people (first_name, last_name, birthdate)
  VALUES ('Paul', 'Giamatti', '1967-06-06');
```

After each INSERT is entered, the terminal will respond with:

```sql
INSERT 0 1
```

</br>

## Selecting the Data

### Selecting all columns from a table:

```sql
SELECT * 
FROM famous_people;
```

### Selecting people with a birthday on or after `'1920-01-01'`

```sql
SELECT * 
FROM famous_people 
WHERE birthdate >= '1920-01-01';
```

### Selecting people based on first name

```sql
SELECT * 
FROM famous_people 
WHERE first_name = 'Paul';
```

### Count total number of people in table:

```sql
SELECT count(*) 
FROM famous_people
```

</br>

## WHERE Clause

| OPERATOR  | DESCRIPTION                           |
|-----------|---------------------------------------|
| =         | Equal                                 |
| >         | Greater than                          |
| <         | Less than                             |
| >=        | Greater than or equal to              |
| <=        | Less than or equal to                 |
| <>        | Not equal. In some versions of SQL this may be written as !=  |
| BETWEEN   | Between a certain range               |
| LIKE      | Search for a pattern                  |
| IN        | To specify multiple possible values for a column  |

These can be added to using `AND`.

```sql
SELECT facid, name, membercost, monthlymaintenance
FROM cd.facilities
WHERE membercost > 0 AND membercost < monthlymaintenance/50; -- 2 WHERE clauses
```

</br>

### Basic String Searches

SQL's `LIKE` operator provides simple pattern matching on strings.

```sql
SELECT *
FROM cd.facilities
WHERE name LIKE '%Tennis%'; -- looks for any match containing "Tennis"
```

The `%` symbol will look for any words on whichever side you place the symbol on. Above it will look for "Tennis" between any words.

</br>

## Sub Queries

In SQL, we can nest a query within another query. We can write a `SELECT` inside of a `SELECT`.

### As a Column in SELECT

If we wanted the total number of incomplete assignments for a specific student. We could take the total number of assignments and subtract the amount submitted by that student. This query however, would require linking three different tables when we really only need the two tables.

We could create two different queries, one for the total number of assignments and the other for total submitted by student.

```sql
SELECT count(*)
FROM assignments; -- results in 424
```
Then subtract the number of assignments the student has submitted.

```sql
SELECT 424 - COUNT(assignment_submissions)
FROM assignment_submissions
JOIN students ON students.id = student_id
WHERE students.name = 'Ibrahim Schimmel';
```
But hard coding the `424` is bad. What if the total number of assignments changes? We can use a sub query here!

```sql
SELECT (
  SELECT count(assignments)
  FROM assignments
) - count(assignment_submissions) as total_incomplete
FROM assignment_submissions
JOIN students ON students.id = student_id
WHERE students.name = 'Ibrahim Schimmel';
```

</br>

### FROM sub select table

The result of a `SELECT` is effectively a table that can be used as you would another table. Therefore a SELECT statement can be used as a data source for another select statement.

```sql
SELECT * FROM (
  SELECT some_id
  FROM some_table
  WHERE something
) AS sub_table;
```

</br>

### Search within a result set IN

IN will search from a list inside the brackets. Example (1, 2, 3). The SELECT statement here will produce a list. Useful when matching against multiple possible values.

```sql
SELECT * FROM table
WHERE id IN (
  SELECT something_id
  FROM someTable
  WHERE something
);
```

Can also be useful when searching for something ***NOT*** in the list.

```sql
SELECT * FROM table
WHERE id NOT IN (
  SELECT something_id
  FROM someTable
  WHERE something
);
```

</br>

A sub query's results can also be used within the `WHERE` clause of a query. This is perhaps the most common way of using a sub select.

We could get a list of IDs for incomplete assignments for a given student:

 ```sql
SELECT assignment_id
FROM assignment_submissions
JOIN students ON students.id = student_id
WHERE students.name = 'Ibrahim Schimmel';
 ```

 This will return a list of ID's of incomplete assignments. Given this list, we just need to get the assignment names of ID's not in this list.

 ```sql
 SELECT assignments.name
FROM assignments 
WHERE id NOT IN
(
  SELECT assignment_id
  FROM assignment_submissions
  JOIN students ON students.id = student_id
  WHERE students.name = 'Ibrahim Schimmel'
);
```

</br>

## Classify Results into Buckets with `CASE`

[pgexercises.com - classify](https://pgexercises.com/questions/basic/classify.html)

`CASE` can be used like an if/switch statement. We can use this to compute what's placed in a column.

```sql
SELECT name, 
	CASE WHEN (monthlymaintenance > 100) THEN 'expensive'
	ELSE 'cheap'
	END AS cost -- "AS" will label the column as "cost"
FROM cd.facilities;  
```

</br>

## `UNION`

If there is ever a need to join information from two tables to the same column, we can use `UNION`.

```sql
SELECT surname
FROM cd.members
UNION
SELECT name
FROM cd.facilities;
```

This will place surnames and facility names into the same 'surname' column.

</br>

# `JOIN`

[A Visual Explanation of SQL Joins](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)

[Lighthouse Walk-through on Joins](https://web.compass.lighthouselabs.ca/activities/934)

We use `JOIN` to link multiple tables together. We link using the FK.

> Every `JOIN` ***must** have an `ON` to link the tables

```sql
SELECT starttime
FROM cd.bookings
JOIN cd.members ON cd.bookings.memid = cd.members.memid 
-- linking the id from members to the FK member id in the bookings table
WHERE cd.members.firstname = 'David'
	AND cd.members.surname = 'Farrell';
```

The most commonly used join is `INNER JOIN`. INNER JOIN will only return records that match from both tables. As above, we can omit the 'INNER', SQL knows that JOIN referes to 'INNER'.

There are also `OUTER` JOINS - `LEFT OUTER JOIN`, `RIGHT OUTER JOIN`, and `FULL OUTER JOIN`. Similar to INNER, we can omit the OUTER and just use `LEFT JOIN` etc.

Unlike INNER JOIN, the OUTER JOINS will return records where there is no matching data.

</br>

## LEFT OUTER JOIN

```sql
FROM students LEFT JOIN cohorts ON cohorts.id = cohort_id
```

```
+-----------------------------------------------------------+ 
  student_name   |            email            | cohort_name 
+----------------+-----------------------------+------------+
 Stephanie Wolff | darius.homenick@tod.ca      | FEB12
 Armand Hilll    | lera_hahn@dickens.org       | FEB12
 Sally Bayer     | kuhic.opal@wuckert.tv       | MAR12
 Magdalena Rau   | nedra.parisian@yahoo.com    | MAR12
 Okey Jaskolski  | mcdermott.jack@yahoo.com    | APR09
 Jeramie Volkman | lucile.lynch@abbie.tv       | 
 Hadley Corkery  | adaline_gutkowski@green.org | 
+-----------------------------------------------------------+ 
```

</br>

## RIGHT OUTER JOIN
```sql
FROM students RIGHT JOIN cohorts ON cohorts.id = cohort_id
```
```
+-----------------------------------------------------------+ 
  student_name   |            email            | cohort_name 
+----------------+-----------------------------+------------+
 Stephanie Wolff | darius.homenick@tod.ca      | FEB12
 Armand Hilll    | lera_hahn@dickens.org       | FEB12
 Sally Bayer     | kuhic.opal@wuckert.tv       | MAR12
 Magdalena Rau   | nedra.parisian@yahoo.com    | MAR12
 Okey Jaskolski  | mcdermott.jack@yahoo.com    | APR09
                 |                             | DEC17
+-----------------------------------------------------------+ 
```

</br>

## FULL OUTER JOIN

```sql
FROM students FULL OUTER JOIN cohorts ON cohorts.id = cohort_id
```
```
+-----------------------------------------------------------+ 
  student_name   |            email            | cohort_name 
+----------------+-----------------------------+------------+
 Stephanie Wolff | darius.homenick@tod.ca      | FEB12
 Armand Hilll    | lera_hahn@dickens.org       | FEB12
 Sally Bayer     | kuhic.opal@wuckert.tv       | MAR12
 Magdalena Rau   | nedra.parisian@yahoo.com    | MAR12
 Okey Jaskolski  | mcdermott.jack@yahoo.com    | APR09
 Jeramie Volkman | lucile.lynch@abbie.tv       | 
 Hadley Corkery  | adaline_gutkowski@green.org | 
                 |                             | DEC17
+-----------------------------------------------------------+ 
```

<br>

[Lighthouse - W05D1](https://web.compass.lighthouselabs.ca/days/w05d1)