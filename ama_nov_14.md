### 1. What is polymorphism

One interface, many forms: The same method name or operation behaves differently depending on the object. In Python it shows up as method overriding and duck typing.

### 2. What is an alternate key in SQL?

A candidate key that wasn’t chosen as the primary key. A table can have several columns that uniquely identify a row, such as id, email, and phone. If id is the primary key, then email and phone are alternate keys. They’re usually declared UNIQUE.

### 3. What happens if a child class method has the same name as a parent method?

The child’s version overrides the parent’s. Calling the method on a child object runs the child’s code. We can call the parent’s version with super().method().

### 4. Use of LIMIT in SQL

It restricts the number of rows returned. With OFFSET it skips rows first, which is how paging works.

### 5. Use of ANY

It compares a value with a list or subquery and is true if the comparison holds for at least one value.

### 6. What is a decorator?

A function that takes another function and returns a modified version, adding behavior without changing the original code. The @ syntax applies it.

```python
def log(func):
    def wrapper(a,b):
        print("calling", func.__name__)
        return func(a,b)
    return wrapper

@log
def add(a, b):
    return a + b
```

### 7. What is dependency in SQL?

Usually a functional dependency: column B depends on column A (A → B) if each value of A determines exactly one value of B. For example, student_id → student_name. It’s the basis of normalization, which removes partial and transitive dependencies to reduce duplication.

### 8. Ways to check that a value is in a range

- using between and IN clause

```sql
WHERE x BETWEEN 10 AND 20
WHERE x IN (10, 11, 12)
WHERE x = ANY (ARRAY[10, 11, 12])
```

### 9. Difference between row and column

A row (record) is one complete entry, such as one match. A column is one property shared by all rows.

### 10. TCL commands

Transaction Control Language: COMMIT, ROLLBACK, SAVEPOINT, ROLLBACK TO SAVEPOINT, and SET TRANSACTION. BEGIN or START TRANSACTION starts a transaction.

### 11. Filter a movies table where reviews contains “histrionics”

```sql
SELECT * FROM movies WHERE review = 'histrionics';
```

### 12. What is abstraction?

Showing only what’s essential and hiding the implementation details.
You use car.start() without knowing how the engine works.
In Python it’s done with abstract base classes (abc module).

### 13. Use of the WITH clause

It defines a named temporary result that the main query can use. It makes complex queries readable, avoids repeating subqueries, and supports recursion.

```sql
WITH wins AS (
    SELECT winner, COUNT(*) AS n FROM matches GROUP BY winner
)
SELECT * FROM wins WHERE n > 50;
```

### 14. COMMIT vs ROLLBACK

COMMIT makes all changes in the current transaction permanent. ROLLBACK undoes them and returns the data to how it was at the start of the transaction.

### 15. Can you print all the records without SELECT?

```sql
TABLE matches;
```

### 16. What is a cross join?

It pairs every row of the first table with every row of the second (a Cartesian product).
If A has 3 rows and B has 4, the result has 12 rows. There is no ON condition.