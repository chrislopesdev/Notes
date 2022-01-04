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
SELECT * FROM famous_people;
```

### Selecting people with a birthday on or after `'1920-01-01'`

```sql
SELECT * FROM famous_people WHERE birthdate >= '1920-01-01';
```

### Selecting people based on first name

```sql
SELECT * FROM famous_people WHERE first_name = 'Paul';
```

### Count total number of people in table:

```sql
SELECT count(*) FROM famous_people
```

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

```sql
SELECT * FROM table
WHERE id IN (
  SELECT something_id
  FROM someTable
  WHERE something
);
```

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

<br>

[Lighthouse - W05D1](https://web.compass.lighthouselabs.ca/days/w05d1)