# DATA DEFINITION LANGUAGE

The SQL commands that we use to define the database schema are sometimes referred to as Data Definition Language (DDL) statements. Some of the most common DDL statements are `CREATE`, `ALTER`, and `DROP`. These can be used to create, modify, and remove database objects such as tables, indexes, and users.

<br>

## Creating Tables

Each box in an ERD will be a table in the database. Each row in the ERD will be a column in the table. If we had the following entity in our ERD:

```
+--------------+
| users        |
+--------------+
| id           |
| name         |
| birth_year   |
| member_since |
+--------------+
```

Our `CREATE TABLE` statement would look something like this:

```sql
CREATE TABLE users (
  id PRIMARY KEY,
  name,
  birth_year,
  member_since
);
```

> This will give an error because we haven't specified the data type

```sql
ERROR:  syntax error at or near "PRIMARY"
```

<br>

## Data Types

> 🔗 [PostgreSQL Docs on Data Types](https://www.postgresql.org/docs/9.3/datatype.html)

> 🔗 [PostgreSQL Data Types](https://www.postgresqltutorial.com/postgresql-data-types/)

SQL has many more data types than JavaScript. In JavaScript a `10` or `3.14` can be stored as `number`. In PostgreSQL, we ***must*** choose from the following ***ten*** numeric types: `SMALLINT`, `INTEGER`, `BIGINT`, `DECIMAL`, `NUMERIC`, `REAL`, `DOUBLE`, `SMALLSERIAL`, `SERIAL`, `BIGSERIAL`.

This allows the database to be more efficient when storing and sorting our data.

### Common Number Types
* ***SMALLINT*** -32,768 to 32,767 (thirty-two thousand)
* ***INTEGER*** -2,147,483,648 to 2,147,483,647 (two billion)
* ***BIGINT*** -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (nine quintillion)
* ***SERIAL*** 1 to 2,147,483,647 (auto incrementing)

### Dates
Dates use [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date formatting standards 'YYYY-MM-DD'

### Phone Numbers
Store as VARCHAR, there are so many possible formats. The number `214 748 3647` hits our `INTEGER` limit.

### Currency
Store currency as an integer representing cents. Use a `BIGINT` if you need values over $21 million dollars.

<br>

## Altering a Table

Sometimes we may have created a table but need to add more columns. We have two options:
1. We can alter the `users` table to add the new columns
2. We can `drop` the `users` table completely and re-create it

Some of the things we can do to alter our table:
* Add or remove a column
* Change an existing column type
* Add or remove an index

> 🔗 [PostgreSQL ALTER TABLE](https://www.postgresqltutorial.com/postgresql-alter-table/)

We can add columns with `ADD COLUMN`:

```sql
ALTER TABLE users
ADD COLUMN name VARCHAR(255), 
ADD COLUMN  birth_year SMALLINT, 
ADD COLUMN  member_since TIMESTAMP
```

To view the new table schema we can run `\d users` in the terminal.

<br>

## Removing a Table

This can be dangerous, but if we need to remove a table, we can use `DROP TABLE`. Doing this will ***remove all data*** from the table as well.

```sql
DROP TABLE users;
```

If we have other tables in our database that depend on this table, we can remove those records using `CASCADE`.

```sql
DROP TABLE users CASCADE;
```

To avoid errors, it's good to check that the table exists before dropping it.

```sql
DROP TABLE IF EXISTS users CASCADE;
```

<br>

## NULL

If we add a row to a table and don't include a value for a column, that value is NULL.

```
id | name | birth_year | member_since
----+------+------------+--------------
  1 |      |       2019 |
```

The empty spaces in the table above represent `NULL` values. To avoid this we can mark a column as `NOT NULL`.

```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY NOT NULL,
  name VARCHAR(255) NOT NULL,
  birth_year SMALLINT NOT NULL,
  member_since TIMESTAMP NOT NULL
);
```

<br>

## Default Values

We can add a default to a table column and if we omit the data when adding the row it will use the default.

```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY NOT NULL,
  name VARCHAR(255) NOT NULL,
  birth_year SMALLINT NOT NULL,
  member_since TIMESTAMP NOT NULL DEFAULT Now()
);
```

```sql
INSERT INTO users (id, name, birth_year) -- we omitted the member_since data
VALUES (2, 'Malloy Jenkins', 1000);
```

<br>

## Auto Incrementing / Serial

The value for the id column needs to be unique. Having it increment is a good way to always have a new unique id. In PostgreSQL we can set the type to be `SERIAL`. This is a pseudo-type that sets the column to be a `NOT NULL INTEGER` that's value will auto-increment.

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY, -- creates an auto-incrementing integer
  name VARCHAR(255) NOT NULL,
  birth_year SMALLINT NOT NULL,
  member_since TIMESTAMP NOT NULL DEFAULT Now()
);
```

<br>

## Foreign Keys

Our users now need to own many pets, we're going to need a `pets` table. Because a user can have ***many*** pets, the pets table will need a special column to reference their owner's id. This column will be a `foreign key` column because it references the `primary key`.

```sql
CREATE TABLE pets (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  owner_id INTEGER NOT NULL REFERENCES users(id)
);
```

There is an issue with the above table. If we delete a user, we will have an error because the pet data references the user's id. What we want to happen, is that if a user is deleted, their pet should be removed as well. We can do this with the following:

```sql
CREATE TABLE pets (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  owner_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE
);
```

Adding `ON DELETE CASCADE` to a foreign key ensures that the row will be deleted when the data it's referencing is deleted.