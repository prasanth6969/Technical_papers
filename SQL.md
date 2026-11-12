## SQL ##
- SQL means Structured Query Language.
- SQL has many databases like MySQL, PostgreSQL, SQLite etc.
- If you want to create a database, keep these in mind:
  - What kind of thing are we storing?
  - What properties does this thing have?
  - What type of data does each property contain? (data types like strings or numbers)

## Creating a Table ##
```sql
CREATE TABLE cities(
  name VARCHAR(50),
  country VARCHAR(50),
  population INTEGER,
  area INTEGER
);
```
In the above example:
- **keyword** = CREATE TABLE
- **identifier** = cities
- name, country, population, area are columns
- VARCHAR(50) = text that can store up to 50 characters
- INTEGER = a number without a decimal

**Inserting data**
```sql
INSERT INTO cities(name, country, population, area)
VALUES ('Tokyo', 'Japan', 81265763, 1000);
```

---

## Important Statements ##

### Reading data ###
- `SELECT` : chooses which columns you want to see.
- `SELECT *` : shows all columns.
- `FROM` : tells which table the data comes from.
- `WHERE` : keeps only the rows that match a condition.
- `DISTINCT` : removes duplicate rows from the result.
- `ORDER BY` : sorts the result (`ASC` small to big, `DESC` big to small).
- `LIMIT` : returns only the first N rows.
- `OFFSET` : skips the first N rows before returning.
- `AS` : gives a column or table a nicer temporary name (alias).

### Combining conditions ###
- `AND` : both conditions must be true.
- `OR` : at least one condition must be true.
- `BETWEEN` : value is inside a range (both ends included).
- `IN (...)` : value matches anything in a list.
- `NOT IN (...)` : value matches nothing in the list.

### NULL (missing values) ###
- `NULL` : means "no value" (it is not 0 and not an empty string).
- `IS NULL` : finds rows where the value is missing (`= NULL` never works).
- `IS NOT NULL` : finds rows where a value exists.
- `COALESCE(a, b)` : replaces NULL with a default value.

### Math and expressions ###
- `+ - * /` : basic math on columns.
- `%` (modulo) : gives the remainder after division.

### Joining tables ###
- `JOIN` / `INNER JOIN` : combines two tables and keeps only rows that match in both.
- `LEFT JOIN` : keeps all rows from the left table, even with no match (gives NULL).
- `RIGHT JOIN` : keeps all rows from the right table, even with no match.
- `FULL JOIN` : keeps all rows from both tables.
- `ON` : says which columns link the two tables.

### Grouping ###
- `GROUP BY` : puts rows with the same value into one group, so you can calculate per group.
- `HAVING` : filters groups after grouping (use it for `COUNT`, `SUM`, `AVG` conditions).

### Changing data ###
- `INSERT INTO` : adds a new row to a table.
- `VALUES` : gives the actual values for the new row.
- `UPDATE` : changes values in existing rows (always use `WHERE`, or every row changes).
- `SET` : says which column gets which new value (separate several with commas).
- `DELETE FROM` : removes rows from a table (always use `WHERE`, or every row is deleted).

### Changing tables ###
- `CREATE TABLE` : makes a new table with its columns and data types.
- `CREATE TABLE IF NOT EXISTS` : makes the table only if it is not already there.
- `ALTER TABLE ... ADD` : adds a new column to a table.
- `ALTER TABLE ... DROP COLUMN` : removes a column from a table.
- `ALTER TABLE ... RENAME TO` : changes the name of a table.
- `DROP TABLE` : deletes the whole table and all its data.
- `DROP TABLE IF EXISTS` : deletes the table only if it exists (no error if it doesn't).

### Column rules (used inside CREATE TABLE) ###
- `PRIMARY KEY` : makes the column a unique id for each row.
- `NOT NULL` : the column cannot be left empty.
- `DEFAULT` : the value used when none is given.
- `UNIQUE` : no two rows can have the same value in this column.

### ALTER, UPDATE, DELETE, DROP ###
- `ALTER TABLE t ADD col type` : adds a new column to the table.
- `ALTER TABLE t DROP COLUMN col` : removes a column and all its data.
- `ALTER TABLE t RENAME TO new_name` : changes the name of the table.
- `UPDATE t SET col = value WHERE condition` : changes the values in existing rows.
- `DELETE FROM t WHERE condition` : deletes only the rows that match; the table stays.
- `DELETE FROM t` : deletes all rows; the empty table stays.
- `DROP TABLE t` : deletes the whole table (rows and structure) completely.
- `ALTER` changes the table structure, `UPDATE` changes the data, `DELETE` removes rows, `DROP` removes the table itself.

---

## Some Operators ##
| Operator | Condition | Example |
|---|---|---|
| `=` | Case sensitive exact string comparison (notice the single equals) | `col_name = "abc"` |
| `!=` or `<>` | Case sensitive exact string inequality comparison | `col_name != "abcd"` |
| `LIKE` | Case insensitive exact string comparison | `col_name LIKE "ABC"` |
| `NOT LIKE` | Case insensitive exact string inequality comparison | `col_name NOT LIKE "ABCD"` |
| `%` | Used anywhere in a string to match a sequence of zero or more characters (only with `LIKE` or `NOT LIKE`) | `col_name LIKE "%AT%"` (matches "AT", "ATTIC", "CAT" or even "BATS") |
| `_` | Used anywhere in a string to match a single character (only with `LIKE` or `NOT LIKE`) | `col_name LIKE "AN_"` (matches "AND", but not "AN") |
| `IN (…)` | String exists in a list | `col_name IN ("A", "B", "C")` |
| `NOT IN (…)` | String does not exist in a list | `col_name NOT IN ("D", "E", "F")` |

**Select query with ordered results**
```sql
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```

**Select query with limit and offset**
```sql
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```
- OFFSET = where to start
- LIMIT = number of rows to print

### Aggregate functions ###
- An aggregate function is a function that performs a calculation on a set of values, and returns a single value.
- MIN() - returns the smallest value of a column
- MAX() - returns the largest value of a column
- COUNT() - returns the number of rows in a set (`COUNT(*)` counts all rows, `COUNT(column)` skips NULLs)
- SUM() - returns the sum of a numerical column
- AVG() - returns the average value of a numerical column

## Order of a Full Query ##
```sql
SELECT column, AGGREGATE(column)
FROM table
JOIN other_table ON table.id = other_table.table_id
WHERE row_condition
GROUP BY column
HAVING group_condition
ORDER BY column
LIMIT n OFFSET m;
```
- `WHERE` filters rows **before** grouping.
- `HAVING` filters groups **after** grouping.

## Flow of Execution ##
SQL does not run a query in the order you write it. It runs in this order:
1. `FROM` / `JOIN` : first picks the table(s) and joins them together.
2. `WHERE` : filters the rows.
3. `GROUP BY` : puts the remaining rows into groups.
4. `HAVING` : filters the groups.
5. `SELECT` : picks the columns and calculates expressions, aggregates and aliases.
6. `DISTINCT` : removes duplicate rows.
7. `ORDER BY` : sorts the result.
8. `LIMIT` / `OFFSET` : keeps only the rows you asked for.
- Because `SELECT` runs after `WHERE`, you can't use an alias from `SELECT` inside `WHERE`.
- Because `ORDER BY` runs after `SELECT`, you can use an alias there.
- `WHERE` can't use `SUM` or `COUNT`, because groups don't exist yet; use `HAVING`.