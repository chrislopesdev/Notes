# ENTITY RELATIONSHIP DESIGN

[ERD on Wikipedia](https://en.wikipedia.org/wiki/Database_design)

Database design is the organization of data according to a database model. The designer determines what data must be stored and how the data elements interrelate. With this information, they can begin to fit the data to the database model. Database management system manages the data accordingly.

Database design involves classifying data and identifying interrelationships. This theoretical representation of the data is called an ontology. The ontology is the theory behind the database's design.

<br>

## DESIGN PROCESS

1. ***Determine the purpose of the database*** - This helps prepare for the remaining steps.
2. ***Find and organize the information required*** - Gather all of the types of information to record in the database, such as product name and order number.
3. ***Divide the information into tables*** - Divide information items into major entities or subjects, such as Products or Orders. Each subject then becomes a table.
4. ***Turn information items into columns*** - Decide what information needs to be stored in each table. Each item becomes a field, and is displayed as a column in the table. For example, an Employees table might include fields such as Last Name and Hire Date.
5. ***Specify primary keys*** - Choose each table's primary key. The primary key is a column, or a set of columns, that is used to uniquely identify each row. An example might be Product ID or Order ID.
6. ***Set up the table relationships*** - Look at each table and decide how the data in one table is related to the data in other tables. Add fields to tables or create new tables to clarify the relationships, as necessary.
7. ***Refine the design*** - Analyze the design for errors. Create tables and add a few records of sample data. Check if results come from the tables as expected. Make adjustments to the design, as needed.
8. ***Apply the normalization rules*** - Apply the data normalization rules to see if tables are structured correctly. Make adjustments to the tables, as needed.

<br>

## Normalization

In the field of relational database design, normalization is a systematic way of ensuring that a database structure is suitable for general-purpose querying and free of certain undesirable characteristics—insertion, update, and deletion anomalies that could lead to loss of data integrity.

### Denormalized Database

```
+-------------------------------------+
| students                            |
+-------------------------------------+
| id | name             | cohort_name |
+-------------------------------------+
| 1   | Sam Billings    | FEB12       |
| 2   | Susan Hudson    | MAR15       |
| 3   | Mallory Jenk    | APR09       |
| 4   | Maximus Ales    | APR09       |
| 5   | Pegasus Laru    | APR09       |
+-------------------------------------+
```

We would consider this denormalized because the cohort name is repeated for 3 of the students. In order to normalize this database we would split the data into two related tables. If a cohort name changes, then we must update all rows with than name. This can get incredibly complex, especially for larger databases.

### Normalized Database
```
+-------------------------------------+   +-------------+
| students                            |   | cohorts     |
+-------------------------------------+   +-------------+
| id | name             | cohort_id   |   | id  | name  |
+-------------------------------------+   +-------------+
| 1   | Sam Billings    | 1           |   | 1   | FEB12 |
| 2   | Susan Hudson    | 2           |   | 2   | MAR15 |
| 3   | Mallory Jenk    | 3           |   | 3   | APR09 |
| 4   | Maximus Ales    | 3           |   +-------------+
| 5   | Pegasus Laru    | 3           |
+-------------------------------------+
```

We still show that each student belongs to a cohort, but the details of the cohort are stored separately. When we need to gather this information together, we use a query to ask the database for it in the structure that we want. This is when we start joining tables together.

If we needed to change the name of a cohort for any reason we only need to change the one field in the cohorts table.

<br>

# RELATIONSHIPS BETWEEN TABLES

## One to Many

Does a student have many cohorts, or does a cohort have many students?

Asking questions about your objects allows you to better understand their relationships. Obviously a student will not have many cohorts so there is a one-to-many relationship with the cohort to students.

```
        MANY                            ONE
+-----------------+            +-----------------+
|     students    |            |     cohorts     |
+-----------------+            +-----------------+
| PK | id         |       /----| PK | id         |
|    | name       |      /     |    | name       |
|    | email      |\    /      |    | start_date |
| FK | cohort_id  |----/       |    | end_date   |
|    | start_date |/           +-----------------+
|    | end_date   |
+-----------------+
```

> ***THE FOREIGN KEY is on the MANY side!***<br>
> ***THE FOREIGN KEY is on the MANY side!***<br>
> ***THE FOREIGN KEY is on the MANY side!***<br>

<br>

## Many to Many

Imagine our requirements change and a student can now have ***many*** cohorts. This is now a `many-to-many` relationship. In a relational database, there is no way to directly model a many-to-many relationship. Instead, we turn this into ***two*** one-to-many relationships using a `join` table.

```
       ONE                         MANY                      ONE
+-----------------+        +-----------------+       +-----------------+
|     students    |        | cohorts_students|       |     cohorts     |
+-----------------+        +-----------------+       +-----------------+
| PK | id         |--\     | PK | id         |\   /--| PK | id         |
|    | name       |   \   /| FK | cohort_id  |---/   |    | name       |
|    | email      |    \---| FK | student_id |/      |    | start_date |
| FK | cohort_id  |       \+-----------------+       |    | end_date   |
|    | start_date |                                  +-----------------+
|    | end_date   |
+-----------------+
```

This is a very basic example where our join table only contains two foreign keys. But it could contain many foreign keys and any other data that would help model our relationship.

