---
title: SQL Basics
author: Alex Nussbacher and Tauhida Parveen
team: grading
time: 90 minutes
uuid: 7adf65cf-8fd6-4b9d-84c5-7e945fcdf3c6
---

We're now ready to begin learning SQL statements for creating and querying (that is, looking for data in) database tables. As a data scientist, database queries are the foundation on which much of your work will rest: in order to analyze and model data, you first need to get the *right* data, and SQL provides a rich set of statements that can be combined to precisely specify the data you want to retrieve from a database. 

In this checkpoint, we'll cover the basics, and at the end you'll work through a series of drills where you practice SQL basics.

Here are the topics we'll cover:

* creating tables
* querying tables
* filtering queries
* ordering query results
* aliasing
* limiting query results
* formatting conventions for SQL queries

## The `CREATE` clause

Earlier when you initially installed and set up Postgres, we came across the terms *schema* and *table*. A database *schema* is a formal statement in SQL about how the tables and columns for a database are set up. A database contains one or more schemas, which in turn contain tables. Schemas also contain other kinds of objects, including data types, functions, and operators. The term schema can also refer to a particular table's configuration of columns. 

To create a new table in your database, you use the `CREATE TABLE` clause. The syntax for creating a table looks as follows:

```sql
CREATE TABLE table_name (
 some_column_name TYPE column_constraint,
 some_other_column_name TYPE,
 yet_another_column_name TYPE
);
```

You need to specify the name of the table after the `CREATE TABLE` clause. To avoid any issues with creating tables, follow a few good conventions: 

* Use lowercase for table names
* Don’t use spaces in table names. If you have more than one word for a table name, combine them using an underscore (_). For example, `lower_case_and_underscore`
* Postgres has some oddities around naming identifiers (such as table names) in quotes and non-quotes. Suffice to say: Avoid using double quotes in your table names! 
* Use meaningful table names and be consistent.

If you want to know more about identifier naming conventions, refer to [the Postgres documentation](https://www.postgresql.org/docs/current/static/sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS).

The lines after the `CREATE TABLE table_name` statement configure individual columns. Each column has a name (following the same conventions as we used for table names). Each column also must list its type (to be clear, `TYPE` above is just a placeholder, you would need to use an actual type like `TEXT` or `INTEGER`.

At a minimimum, each column must have a name and a type, but it's also possible to add [constraints](https://www.postgresql.org/docs/current/static/ddl-constraints.html) to columns such as making values in a column unique for the table, or probiting null values.

The individual column creation lines in our SQL statement get separated by a comma (and a new line, but this is not strictly speaking necessary, it's a convention that ensures readability).

Postgres includes a large set of built-in data types. Depending on the data that will be stored in the columns, you have to choose the correct data type for the data. You can also define your own data type, but with the rich data types that are provided by Postgres, there is often not a need for defining your own data type. Also, you will notice that sometimes the data types are written in UPPER CASE. It is not mandatory but a convention that the keywords (SQL statements, data types etc.) are written in lowercase and identifiers (table names, operations etc.) are written in lower case.  When creating a table schema, you should consult [this Postgres data type table](https://www.postgresql.org/docs/current/static/datatype.html) to choose the correct data type for your data.

Earlier, you created the BikeShare database using table schemas provided to you. Now that you know more about tables Open the weather.sql in either pgadmin or your favorite code editor (e.g., VC code, xcode, textmate etc. ) and see if you can understand how the create statement for the weather table is written.



## The `SELECT` and `FROM` clause

The `select` clause retrieves rows of data from a table. The `select` clause includes: a **select** statement and a **from** statement. A minimal SQL query can be made with just these two clauses:

```sql
SELECT * FROM someTable;
```

This query retrieves all columns and rows from someTable. It's saying "Give me all of the values for each of the columns for each row in someTable".

We can also be specific about which columns we want:

```sql
SELECT col1, col2, anotherColumn FROM someTable;
```

Let's try a simple one on our `Bikeshare` database. We will create a query to retrieve the *names* of the stations. 

In pgAdmin, right click on your `Bikeshare` database and select `Query Tools...`. Then run the following query.

```sql
SELECT
    name
FROM
    stations;
```

This query will the name value for each record in the stations table.

![station names](station_names.png)


###### Notice that the `SELECT` and `FROM` keywords are all caps. These days we have fancy text editors with syntax highlighting features that make code easier to read. SQL comes from an era before syntax highlighting was a thing and SQL keywords are conventionally written in all caps to make it easier to differentiate keywords and have more readable code. This convention persists through today. Your SQL will run just fine no matter what capitalization you use, but it enhances readability if you use the capitalization. 

There are a few more options we can use here to make even these basic queries a little easier to execute. First, we can *alias* columns. This refers to referring to the underlying column name in the DB by an alternate name in our database query.

```sql
SELECT
    name station_name
FROM
    stations;
```

This can be more verbosely written as:

```sql
SELECT 
    name AS station_name
FROM
    stations;
```

Column aliasing is particularly useful when you need to query across multiple tables that contain common column names. For example, two tables may each have a column named "id", and we need the "id" values from both tables. Renaming is also valuable when using functions, a more advanced concept to cover later.

It is also worth mentioning `*` here. Many times writing a query means you inherently only want _some_ of the information in a given table. On occasion, however, you want _all_ of the columns present. Rather than typing out every specific column name, SQL gives you the option of using the traditional wildcard of `*` to select all columns. It would look something like this:

```sql
SELECT
    *
FROM
    stations;
```

That will return the entire `station` table. Selecting an entire table is pretty safe when working with small tables like this one, but be careful using this on larger tables. Sometimes it will just be far too much data, and your query can hang. Also, note that when using `*` there is no way to alias columns.

## Filtering with `WHERE`

On their own, as we've seen, the `SELECT` and `FROM` clauses allow us to query some or all of the values for all of the rows in a table. But what if we are interested only in rows meeting a particular condition? For instance, we might want to see all of the orders that reference some specific customer's customer id. Or we might be interested in banking transactions before a certain date.

This is where the `WHERE` clause comes in. The `WHERE` clause lets us specify a set of conditions about how the records we're interested should look. `WHERE` clauses give us the ability to check if one or more conditions are the case, using comparison operators (`=`, `>`, `>=`, etc.).

The [`LIKE` operator](https://www.postgresql.org/docs/current/static/functions-matching.html#FUNCTIONS-LIKE) can be used to use pattern matching when analyzing string data.

[`BETWEEN`](https://www.postgresql.org/docs/current/static/functions-comparison.html) can be used to check if a value is between a set of values. 

And of course, there's always good ole `AND` and `OR` let us link together filter conditions in a `WHERE` block.

## Ordering with `ORDER`

`ORDER BY` allows us to control the order in which data is returned. You can order by one or more columns, specifying either ascending or descending order.

In the following example, we retrieve the trip ID and start date for each trip record in our trips table that where the bike_id column's value is 27 and the zip_code column's value is 94107. In the `ORDER BY` clause, we say that we want this data sorted by the value of the duration column, in descending order.


```sql
SELECT
    trip_id,
    start_date
FROM
    trips
WHERE
    bike_id = 27 AND
    zip_code = 94107
ORDER BY duration DESC;

-- These are comments, by the way. Use two dashes for single-line comments.
```

Run the above statement in your query tool. Note that our conditions here rely on the fact that the columns `bike_id` and `zip_code` are numeric. If you were matching on strings, you would have to compare with a string, which would be enclosed in single quotes (`'`). You might also find the `LIKE` operator useful. 

Here's how the above query might look if we wanted to add a constraint such as `subscriber type`, which is stored in the database as a string:

```sql
SELECT
    trip_id,
    start_date
FROM
    trips
WHERE
    bike_id = 27 AND
	subscriber_type LIKE 'Customer'
ORDER BY duration DESC;
``` 

###### Unlike Python, strings in SQL <em>cannot</em> use double quotes. Keep all your SQL strings using single quotes. Accidentally using double quotes is a common mistake when writing SQL and will give you fun errors.


## Limiting with `LIMIT`

The **limit** clause — `LIMIT` — allows us to limit the number of returned results.

Let's add a limit to an earlier query. Let's get the three longest trips in our table:

```sql
SELECT
    trip_id,
    start_date
FROM
    trips
WHERE 
    bike_id = 27 AND
	subscriber_type LIKE 'Customer'
ORDER BY duration DESC
LIMIT 3;
 ```


## Formatting conventions for SQL queries

SQL is one of the more readable computer languages. By following some common voluntary but recommended stylistic conventions, you can optimize for readability.

Here are some pointers:

1. Put each column name in a select clause on its own line, with one level of indentation from the preceding line.
1. Follow the same indentation logic for `FROM`, `WHERE`, and `ORDER BY` blocks, giving each element its own line.
1. Similarly, each clause gets its own line.
1. Use all caps for clauses, function names, and the like.
1. Use the actual case of the column/table name when referring to column and table names.
1. Be consistent in your own use of casing, but recognize that SQL is not case sensitive, and it doesn't actually care about tabs and newlines.

So the following line will execute, but it's not very readable, and for larger queries will be impossible to thoughtfully debug. You should avoid writing queries in this manner. 

```sql
select trip_id, start_date from trips where bike_id=27 and zip_code=94107 order by duration desc limit 3;
```

## Assignments

Let's confirm some of this new knowledge with a few basic exercises. Write SQL queries to return:

 * The IDs and durations for all trips of duration greater than 500, ordered by duration.
 * Every column of the `stations` table for station id 84.
 * The min temperatures of all the occurrences of rain in zip 94301.

Save your SQL queries in a gist or a GitHub repository and submit a link below.

