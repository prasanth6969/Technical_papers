## Aggrgate Functions ## 
- By using this we perform calculations on multiple values.
- It takes whole columns and return a single value.
- These are used generally in day to day activities like temperature  weather reports etc.
- It ignores NULL except for the count()

## Types of aggregate functions ## 
- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

## GROUP BY ##
GROUP BY takes rows with same value and group them into one value 
- Without this aggregate functions turns whole column into one value that doesnt maek sense
- IN simple words this function divides like IT , DOCTOR columns seprate them and perform operation indepently.

## HAVING ##
- This HAVING function is used to filter the value or category which comes form group by with some certain conditions.

```
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 40000;

```
## JOINS ##

- Joins these are one of the fundamental opertions in SQL .
- we use JOINS when you want to work with mutliple tables.
- WE need *common column* in two tables then only we can make a connection.
- **Inner Join** - This returns only the matching id or matching elements from both table.
**syntax**
```
SELECT T1.name , t2.number 
FROM T1 INNER JOIN t2 ON t1.id = t2.id

```
- **LEFT Join** - This returns matching rows along with all rows with NULL value from left table.
**syntax**
```
SELECT T1.name , t2.number 
FROM T1 LEFT JOIN t2 ON t1.id = t2.id

``` 
- **RIGHT Join** - This returns matching rows along with all rows with NULL value from Right table.
**syntax**
```
SELECT T1.name , t2.number 
FROM T1 RIGHT JOIN t2 ON t1.id = t2.id

```
- **FULL Join** - This returns matching rows and unmatch rowws with NULL value from Both tables.
**syntax**
```
SELECT T1.name , t2.number 
FROM T1 FULL JOIN t2 ON t1.id = t2.id

```
## NORMALIZATION ## 
- Normalization is the process of organising tables so that data is not repeated and stays consistent.
Important points to achieve NORMALIZATION.
 1. **NON atomicity***(means only one data for one cell)
 2. **Parital dependency**(means depends on one column IF you order a mutliple products but within single order that is knows as partial dependecy) 
 3. **Transitive dependency*** (mutual dependency  A non-key column must not depend on another non-key column. Here customer_phone depends on customer, not directly on order_id)  
 4. **Internal dependency**(NO two columns should not depend on each other)

### THUMB RULE FOR NORMALIZATION ###

**1NF** = NO atomicity 
**2NF** = 1NF + NO partial dependency 
**3NF** = 2NF + NO Transitive dependency
**BCNF** = 3NF + NO Internal dependency  

### INDEXING ###
- Selection of right\page becomes faster by using this indexing.
- In simple words if you want to retrieve data from messy table it will take more time so that we use indexing.

Idexing type will depend on key and ordering. 
| Type | Meaning |
|---|---|
| Primary index | Created automatically on the primary key |
| Unique index | Fast search plus no duplicates |
| Clustered index | Decides the physical order of rows; only one per table |
| Non-clustered index | Separate structure with pointers; many allowed |
| Composite index | Index on 2 or more columns; column order matters |

| | Clustered | Non-clustered |
|---|---|---|
| Stores | The table data itself, in order | Separate index with pointers |
| Per table | 1 | Many |
| Analogy | Dictionary | Index at the back of a book | 

## TRANSACTIONS ## 
- It is a collections of operations to do single logical unit of work.
- IN simple words to transafer a 100 rupees from one acc to another that is known as single local unit of work but it requires many multiple operations and set of rules is considered.
- Those set of rules is known as ACID properties.

## ACID Properties ## 
- **A (Atomicity)-** Which means we have set of operations if happens all should be happens or none should be happens but it shouldn't be partial complete. 
- All true or All none.
- **C (Consistency)** - It ensures that the correctness after completion of all set  of operartions 
- **I (Isolation)** - If more than one trasactions happens at a same time all transactions should be done Isolated(All transactions should be done individually). 
- **D (Durability)** - All operations should be permanent in database.

**Software managers of acid properties** 
- Atomicity (Transation manager)  
- Correctness (User/App programer) 
- Isolation (concurrency control manager) 
- Durability (recovery manager) 

### Transaction commands ###

| Command | Purpose |
|---|---|
| `BEGIN` / `START TRANSACTION` | Start a transaction |
| `COMMIT` | Save all changes permanently |
| `ROLLBACK` | Undo all changes since the start |
| `SAVEPOINT name` | Mark a point inside the transaction |
| `ROLLBACK TO name` | Undo only back to that savepoint |

### Concurrency Control ### 
- Unconcurrency control leads to a unwanted outputs or database mis manupulation.
- So we need to control the concurrecny we have different types 
 1. Lock-based protocols 
 2. Timestamp based protocols 
 3. Multi- granularity protocols 
 4. Multi-version protocols  

# Concurrency Control Protocols

## 1. Lock-based protocols
Transactions must get a lock on data before using it, so conflicting access is blocked.

- **Simple lock:** Lock before use and unlock when done, with no timing rules. Not safe on its own, because other transactions can see half-finished data.
- **Two-phase locking (2PL):** Acquire all locks first (growing phase), then release them (shrinking phase). It guarantees serializability but can cause deadlocks.
  - **Strict 2PL:** Holds exclusive locks until commit or rollback. Prevents cascading rollbacks.
  - **Rigorous 2PL:** Holds all locks (shared and exclusive) until commit or rollback.
  - **Conservative 2PL:** Takes all locks before the transaction starts. Prevents deadlocks, but needs the locks to be known upfront.
- **Graph-based protocol:** Data is arranged in a tree, and a node can be locked only if its parent is locked. Deadlock-free.

## 2. Timestamp-based protocols
No locks. Each transaction gets a timestamp when it starts, and conflicting operations are ordered by timestamp.

- **Timestamp ordering:** If an operation arrives "too late" compared to a younger transaction's read or write, the transaction is aborted and restarted. Deadlock-free, but may abort often.
- **Thomas write rule:** A modified version that ignores an outdated write instead of aborting. This reduces rollbacks.

## 3. Multi-granularity protocols
Locks can be taken at different levels (database, table, page, row), using intention locks on the higher levels.

- **Intention shared (IS):** "I will take shared locks on some rows below."
- **Intention exclusive (IX):** "I will take exclusive locks on some rows below."
- **Shared intention exclusive (SIX):** Shared lock on the whole node, plus intention to take exclusive locks on rows below.

## 4. Multi-version protocols
The database keeps several versions of each data item, so readers read an older version while writers create a new one. Readers and writers don't block each other.

- **Multiversion timestamp ordering:** Each write creates a new timestamped version, and a read picks the latest version older than the reader's timestamp.
- **Multiversion 2PL:** Update transactions use 2PL, while read-only transactions read a snapshot.
- **Snapshot isolation (MVCC):** Each transaction sees a consistent snapshot of the data from when it started. Used by PostgreSQL, Oracle and MySQL InnoDB.

## Isolation Level and Violations ## 
- Isolation levels control how much one transaction can see of the changes made by other transactions running at the same time.
- **Dirty read** - If an item is read without commit is known as Dirty read.
- If T1 isn't committed yet but t2 reads if t1 fails then t2 doesn't care about that.

- **Non-repeatable Read** - Lets consider if data item has value 10 while reading t1 initially after t2 modifies that again t1 reads the value has changed so that causes unwanted outputs.

- **Phantom** - If T1 retrieves data eith some specifc conditions at the same time t2 modify or add another row which again t1 runs it return new phantom row 

**Types of isolation level** 
1. Read uncommitted
2. Read committed 
3. Repeatable Read 
4. serialaizable (Which doesn't allow any type of violation)

### TRIGGER ### 
- Triggers is block of sql code that automatically executes when a specific event happens in a table.
- EXAMPLE - A motion-sensor light. You don’t flip a switch. When someone walks in (the event), the light turns on by itself (the action).

**SYNTAX** 
```
CREATE TRIGGER trigger_name
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON table_name
FOR EACH ROW
BEGIN
    -- SQL statements
END;

```
| Term | Meaning |
|---|---|
| `CREATE TRIGGER` | The command that defines a new trigger |
| `trigger_name` | The name you choose, such as `log_salary_change`. Use something that describes what it does. |
| `{BEFORE \| AFTER}` | When it runs. Pick one. `BEFORE` runs before the change is saved; `AFTER` runs after. |
| `{INSERT \| UPDATE \| DELETE}` | Which event fires it. Pick one. |
| `ON table_name` | The table the trigger is attached to, such as `employees` |
| `FOR EACH ROW` | Run the trigger once for every row affected. If an `UPDATE` changes 5 rows, it runs 5 times. |
| `BEGIN ... END` | The block that holds the trigger's body |
| `-- SQL statements` | The actual work the trigger does (insert into a log, check a value, and so on). `--` starts a comment. | 

- REAL EXAMPLE 
```
CREATE TABLE employe(
    id INT PRIMARY KEY,
    name VARCAHR(50) NOT NULL,
    department VARCHAR(50),
    salary INT
);

CREATE TABLE salary_log(
    log_id = INT AUTO_INCREMENT PRIMARY KEY 
    emp_id INT,
    old_salary INT,
    new_salary INT,
    change_time DATETIME
); 

INSERT INTO employees VALUES
(1, 'Asha',  'IT',    60000),
(2, 'Ravi',  'IT',    50000),
(3, 'Meena', 'HR',    40000); 

CREATE TRIGGER salary_change 
AFTER UPDATE ON employee
FOR EACH ROW 
BEGIN 
IF old.salary <> new.salary THEN 
 INSERT INTO salary_log(emp_id,old_salary,new_salary,change_time)
 VALUES(OLD.id , OLD.salary , NEW.salary,NOW());
 END IF;
END

```
### CAP THEOREM

A distributed database can guarantee only **two of the three** properties below.

- **C: Consistency:** Every read returns the latest write. All nodes show the same data.
- **A: Availability:** Every request gets a response (not an error), even if the data may be slightly old.
- **P: Partition tolerance:** The system keeps working even when the network between nodes drops or delays messages.

Partitions can't be avoided, so the real choice is between **CP** and **AP**:

| Type | During a network failure | 
|---|---|---|
| CP | Returns an error rather than wrong data |
| AP | Always responds, data may be stale | 