# DATA MANIPULATION LANGUAGE

The SQL commands that let us interact with our data are sometimes referred to as Data Manipulation Language (DML). These include:

* `SELECT`: get data from tables
* `INSERT`: add rows to a table
* `UPDATE`: update rows within a table
* `DELETE`: delete rows from a table

<br>

## INSERT

There are two basic syntaxes of the `INSERT INTO` statement:

```sql
INSERT INTO table_name (column1, column2, column3,...columnN)  
VALUES (value1, value2, value3,...valueN);
```

```sql
INSERT INTO table_name VALUES (value1,value2,value3,...valueN);
```

<br>

## DELETE

The basic syntax of the `DELETE` query with the `WHERE` clause is as follows:

```sql
DELETE FROM table_name
WHERE condition; -- always use a WHERE clause when deleting
```

You can combine conditions using `AND` OR `OR` operators.

We usually wouldn't want to delete data from our production database. It would be better to have something like a deleted_at column that stores a DATE. That way we can still filter out deleted results without having to lose the data.

<br>

## UPDATE

The SQL UPDATE Query is used to modify the existing records in a table. You can use the WHERE clause with the UPDATE query to update the selected rows, otherwise all the rows would be affected.

The basic syntax for `UPDATE` with a `WHERE` clause is:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2...
WHERE condition;
```

Example:
```
+----+----------+-----+-----------+----------+
| ID | NAME     | AGE | ADDRESS   | SALARY   |
+----+----------+-----+-----------+----------+
|  1 | Ramesh   |  32 | Ahmedabad |  2000.00 |
|  2 | Khilan   |  25 | Delhi     |  1500.00 |
|  3 | kaushik  |  23 | Kota      |  2000.00 |
|  4 | Chaitali |  25 | Mumbai    |  6500.00 |
|  5 | Hardik   |  27 | Bhopal    |  8500.00 |
|  6 | Komal    |  22 | MP        |  4500.00 |
|  7 | Muffy    |  24 | Indore    | 10000.00 |
+----+----------+-----+-----------+----------+
```

```sql
UPDATE customers
SET address = 'Georgetown'
WHERE id = 6;
```

This will change Komal's address to "Georgetown".

</br>

# BE CAREFUL!

The `UPDATE` and `DELETE` are the most dangerous queries because they change or remove data. This means we need to be very careful when using either of them.

> ⚠️ Never write an `UPDATE` or `DELETE` query without a `WHERE` clause.

