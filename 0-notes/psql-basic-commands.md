# PostgreSQL Cheat Sheet

[PostgreSQL docs](https://www.postgresql.org/docs/current/index.html)

## Basic Commands

Start PostgreSQL from command line:

```
psql
```

Display all available commands:

```
\?
```

Display help information about SQL commands:

```
\h command_name
```

Connect to a database:

```
\c database_name
```

List available databases:

```
\l
```

Display tables:

```
\d
```

Display information about a specific table column:

```
\d table_name column_name
```

List all indexes for a table:

```
\d table_name
```

and look under the "Indexes" section

Toggle aligned format mode (default is aligned):

```
\x
```

Use unaligned format mode when output would be too wide for terminal window, otherwise use aligned mode:

```
\x auto
```

Quit psql mode and return to the command line (also Ctrl+d):

```
\q
```

## Create and delete databases

Create a database:

```
CREATE DATABASE database_name;
```

Delete a database:

```
DROP DATABASE database_name;
```

## Create and delete tables

Create a table:

```
CREATE TABLE table_name();
```

Delete a table:

```
DROP TABLE table_name;
```

Create a table with columns and constraints:

```
CREATE TABLE table_name(column_name DATATYPE CONSTRAINTS, column_name DATATYPE CONSTRAINTS);
```

## Adding, deleting, and renaming columns

Add a column:

```
ALTER TABLE table_name ADD COLUMN column_name DATATYPE;
```

Delete a column:

```
ALTER TABLE table_name DROP COLUMN column_name;
```

Rename a column:

```
ALTER TABLE table_name RENAME COLUMN column_name TO new_name;
```

## Adding and deleting rows

Insert a row:

```
INSERT INTO table_name(column_1, column_2) VALUES(value1, value2);
```

Insert multiple rows:

```
INSERT INTO table_name(column_1, column_2) VALUES(value_1, value_2), (value_1, value_2);
```

Delete a row:

```
DELETE FROM table_name WHERE condition;
```

Truncate a table:

```
TRUNCATE TABLE table_name;
```

## Updating values

Update a value:

```
UPDATE table_name SET column_name=new_value WHERE condition;
```

## Querying data

Select columns from a table:

```
SELECT columns FROM table_name;
```

Select a row based on a condition:

```
SELECT columns FROM table_name WHERE condition;
```

Order by a column:

```
SELECT columns FROM table_name ORDER BY column_name;
```

Join tables:

```
SELECT columns FROM table_1 FULL JOIN table_2 ON table_1.primary_key_column = table_2.foreign_key_column;
```

Join tables in a many-to-many relationship:

```
SELECT columns FROM junction_table
FULL JOIN table_1 ON junction_table.foreign_key_column = table_1.primary_key_column
FULL JOIN table_2 ON junction_table.foreign_key_column = table_2.primary_key_column;
```

## Adding constraints to existing tables

Add a primary key:

```
ALTER TABLE table_name ADD PRIMARY KEY(column_name);
```

Add a foreign key:

```
ALTER TABLE table_name ADD COLUMN column_name DATATYPE REFERENCES referenced_table_name(referenced_column_name);
```

Create a composite primary key:

```
ALTER TABLE table_name ADD PRIMARY KEY(column1, column2);
```

Add a unique constraint:

```
ALTER TABLE table_name ADD UNIQUE(column_name);
```

Add a not null constraint:

```
ALTER TABLE table_name ALTER COLUMN column_name SET NOT NULL;
```

Drop a constraint:

```
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```

Add a column to a table with datatypes, constraints, and references:

```
ALTER TABLE table_name ADD COLUMN column_name DATATYPE CONSTRAINT REFERENCES referenced_table_name(referenced_column_name);
```

## Indexes

Add an index to a column:

```
CREATE INDEX index_name ON table_name(column_name);
```

Drop an index:

```
DROP INDEX index_name;
```

---

## Constraints

| Constraint Type | Syntax                                                                   | Description                                                                                                                                                                                              |
| --------------- | ------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Primary Key     | `PRIMARY KEY (column_name)`                                              | A primary key constraint is used to uniquely identify each row in a table. It is typically defined on one or more columns that are guaranteed to be unique.                                              |
| Foreign Key     | `FOREIGN KEY (column_name) REFERENCES referenced_table(ref_column_name)` | A foreign key constraint is used to ensure that the values in a column match the values in another table's column. It is typically defined on a column that references the primary key of another table. |
| Unique          | `UNIQUE (column_name)`                                                   | A unique constraint is used to ensure that each value in a column is unique. It is typically defined on a column where duplicate values are not allowed.                                                 |
| Not Null        | `NOT NULL`                                                               | A not null constraint is used to ensure that a column always contains a value. It is typically defined on a column where null values are not allowed.                                                    |
| Check           | `CHECK (condition)`                                                      | A check constraint is used to ensure that the values in a column meet a certain condition. It is typically defined on a column where certain values are not allowed.                                     |

---

## Wildcards / special characters

| Wildcard/Special Character | Syntax | Description                                                                                                                                                                                                                                                                                                                |
| -------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Asterisk                   | \*     | Matches any sequence of characters (zero or more) in a string. For example, 'abcd'::text LIKE 'ab%' will return true. In psql, the asterisk wildcard is used in conjunction with the LIKE operator to search for patterns in strings.                                                                                      |
| Percent sign               | %      | Matches any sequence of characters (zero or more) in a string. It is similar to the asterisk wildcard, but is used specifically for pattern matching with LIKE or ILIKE. For example, 'abcd'::text LIKE 'ab%' will return true. In psql, the percent sign wildcard is commonly used for pattern matching in WHERE clauses. |
| Underscore                 | \_     | Matches any single character in a string. For example, 'abcd'::text LIKE '\_\_cd' will return true. In psql, the underscore wildcard is used in conjunction with the LIKE operator to search for patterns that contain a specific character in a specific position.                                                        |
| Question mark              | ?      | Matches any single character in a string. For example, 'abcd'::text LIKE 'a?cd' will return true. In psql, the question mark wildcard is used in conjunction with the LIKE operator to search for patterns that contain a specific character in a specific position, but where the character can be any single character.  |
| Backslash                  | \      | Used as an escape character to treat the next character as a literal character instead of a special character. For example, '\\%' will match the literal characters \%. In psql, the backslash is used to escape special characters in SQL commands or to include special characters in strings.                           |
| Bracket expression         | []     | Matches any single character within the specified range. For example, '[a-d]' matches any character between a and d. In psql, the bracket expression is used with the LIKE operator to search for patterns that contain a range of characters.                                                                             |
| tilde                      | ~      | Matches a regular expression pattern. Example: SELECT \* FROM table_name WHERE column_name ~ 'pattern';                                                                                                                                                                                                                    |
| Caret                      | ^      | Matches any single character not within the specified range. For example, '^[a-d]' matches any character that is not between a and d. In psql, the caret is used with the LIKE operator to search for patterns that do not contain a range of characters.                                                                  |
| Dollar sign                | $      | Matches the end of a line in a multiline string. For example, '^abcd$' matches the string abcd only if it appears on a line by itself. In psql, the dollar sign is used in conjunction with the ~ or ~` operator to search for patterns at the end of lines in multiline strings.                                          |

---

## Logical

| Command     | Description                                                                                                                             |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| LIKE        | Matches a pattern in a string. Example: SELECT \* FROM table_name WHERE column_name LIKE 'pattern';                                     |
| ILIKE       | Case-insensitive version of LIKE.                                                                                                       |
| SIMILAR TO  | Matches a string against a POSIX regular expression pattern. Example: SELECT \* FROM table_name WHERE column_name SIMILAR TO 'pattern'; |
| BETWEEN     | Matches a range of values. Example: SELECT \* FROM table_name WHERE column_name BETWEEN value1 AND value2;                              |
| IN          | Matches a set of values. Example: SELECT \* FROM table_name WHERE column_name IN (value1, value2, value3);                              |
| NOT IN      | Does not match a set of values.                                                                                                         |
| IS NULL     | Matches null values. Example: SELECT \* FROM table_name WHERE column_name IS NULL;                                                      |
| IS NOT NULL | Does not match null values.                                                                                                             |
| AND         | Combines two or more conditions. Example: SELECT \* FROM table_name WHERE condition1 AND condition2;                                    |
| OR          | Either condition1 or condition2 is true.                                                                                                |
| NOT         | Inverts a condition. Example: SELECT \* FROM table_name WHERE column_name NOT NULL;                                                     |

---

## Joins

| Join Type       | Syntax                                                                                    | Description                                                                                                                                                                                   |
| --------------- | ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| INNER JOIN      | `SELECT * FROM table1 INNER JOIN table2 ON table1.column_name = table2.column_name;`      | Inner join returns only the rows that have matching values in both tables.                                                                                                                    |
| LEFT JOIN       | `SELECT * FROM table1 LEFT JOIN table2 ON table1.column_name = table2.column_name;`       | Left join returns all rows from the left table (table1) and matching rows from the right table (table2). If there is no matching row in the right table, the result will contain null values. |
| RIGHT JOIN      | `SELECT * FROM table1 RIGHT JOIN table2 ON table1.column_name = table2.column_name;`      | Right join returns all rows from the right table (table2) and matching rows from the left table (table1). If there is no matching row in the left table, the result will contain null values. |
| FULL OUTER JOIN | `SELECT * FROM table1 FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;` | Full outer join returns all rows from both tables (table1 and table2), and if there are no matching rows in the other table, the result will contain null values.                             |

---
