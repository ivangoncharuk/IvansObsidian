
# Notes comparing SQL and Relational Algebra


---
## Selecting Data

```sql
SELECT * 
FROM Employee;
```

$$\pi_{*}(\text{Employee})$$
- **SQL**: This query retrieves all the data from the `Employee` table.
- **Relational Algebra**: The projection operator $\pi_{*}$ fetches all attributes for every tuple in the `Employee` relation.

---
## Selecting Specific Columns


```sql
SELECT name, age 
FROM Employee;
```

$$\pi_{\text{name, age}}(\text{Employee})$$
- **SQL**: This query retrieves the `name` and `age` columns from the `Employee` table.
- **Relational Algebra**: The projection operator $\pi_{\text{name, age}}$ fetches specified attributes `name` and `age` for every tuple in the `Employee` relation.

---

## Selecting with conditions

```sql
SELECT * 
FROM Employee
WHERE age > 30;
```

$$\sigma_{\text{age > 30}}(\text{Employee})$$
- **SQL**: This query retrieves all data from the `Employee` table where the `age` is greater than 30.
- **Relational Algebra**: The selection operator​ $\sigma_{\text{age > 30}}$ filters the tuples in the `Employee` relation, keeping only those where `age` is greater than 30.
---
## Natural Join

```sql
SELECT * 
FROM Employee
NATURAL JOIN Department;
```

$$\text{Employee} \ \bowtie \ \text{Department}$$
- **SQL**: This query performs a natural join between the `Employee` and `Department` tables, based on common columns.
- **Relational Algebra**: The natural join operator $\bowtie$ combines tuples from `Employee` and `Department` relations based on common attribute values.
---
## Equi-Join

```sql
SELECT * 
FROM Employee
JOIN Department ON Employee.DeptID = Department.DeptID;
```

$$\text{Employee} \bowtie_{\ \text{Employee.DeptID = Department.DeptID}} \ \text{Department}$$
- **SQL**: This query joins the `Employee` and `Department` tables on the `DeptID` column.
- **Relational Algebra**: The equi-join operator $\bowtie_{\text{Employee.DeptID = Department.DeptID}}​$ combines tuples from `Employee` and `Department` relations based on matching values in the `DeptID` attribute.
---

## Grouping

```sql
SELECT DeptID, AVG(salary) 
FROM Employee 
GROUP BY DeptID;
```

$$\gamma_{\ \text{DeptID, AVG(salary)}}(\text{Employee})$$
- **SQL**: This query groups the data in the `Employee` table by `DeptID`, and computes the average salary for each group.
- **Relational Algebra**: The group-by operator $\gamma_{\ \text{DeptID, AVG(salary)}}$​ groups tuples in the `Employee` relation by `DeptID`, and computes the average `salary` for each group.
	- the `GROUP BY` clause is used to arrange identical data into groups. In the given query, employees are grouped based on their `DeptID`, and the average salary is computed for each group. 
	- In relational algebra, the grouping is denoted by the $\gamma$ operator.
---

## Set Operations (Union, Intersection, Difference)

---
### Union

```sql
SELECT * 
FROM Employee 
UNION 
	SELECT * FROM Manager;
```

$$\text{Employee} \ \cup \ \text{Manager}$$
- **SQL (Union)**: This query returns a set of unique rows that appear in either the `Employee` or `Manager` table.
- **Relational Algebra (Union)**: The union operator $\cup$ combines tuples from `Employee` and `Manager` relations, eliminating duplicates.
---
### Intersection

```sql
SELECT * 
FROM Employee 
INTERSECT
	SELECT * FROM Manager;

```

$$\text{Employee} \ \cap \ \text{Manager}$$
- **SQL (Intersection)**: This query returns a set of unique rows that appear in both the `Employee` and `Manager` tables.
- **Relational Algebra (Intersection)**: The intersection operator $\cap$ returns tuples that are present in both `Employee` and `Manager` relations.
---
### Difference

```sql
SELECT * 
FROM Employee 
EXCEPT 
	SELECT * FROM Manager;
```

$$\text{Employee} \ - \ \text{Manager}$$

- **SQL (Difference)**: This query returns a set of unique rows that appear in the `Employee` table but not in the `Manager` table.
- **Relational Algebra (Difference)**: The difference operator $-$ returns tuples that are in the `Employee` relation but not in the `Manager` relation.

---
## Having

```sql
SELECT DeptID, AVG(Salary) 
FROM Employee 
GROUP BY DeptID HAVING AVG(Salary) > 50000;
```

$$\sigma_{\text{AVG(Salary) > 50000}}(\gamma_{\text{DeptID, AVG(Salary)}}(\text{Employee}))$$
- **Explanation:** The `HAVING` clause in SQL is used to filter groups based on a specified condition. 
	- In this query, it filters out groups (departments) where the average salary is greater than 50000. In relational algebra
	- this is represented by applying a selection operator $\sigma$ on the grouped relation.

---

## Ordering

```sql
SELECT Name, Salary 
FROM Employee 
ORDER BY Salary DESC;
```

> There isn't a standard relational algebra expression for ordering, as relational algebra theoretically deals with sets (which are unordered). 
> However, in practice, an extension could be used to denote ordering by using $\tau$ :

$$\tau_{\ \text{Salary DESC}}(\pi_{\ \text{Name, Salary}}(\text{Employee}))$$

- In SQL, the `ORDER BY` clause is used to sort the data in ascending or descending order based on one or more columns. In this query, employees are sorted based on their salary in descending order.

---
## Alias (AS)

```sql
SELECT 
	Name AS EmployeeName, 
	Salary AS EmployeeSalary
FROM Employee;
```

$$\rho_{\ \text{EmployeeName/Name, EmployeeSalary/Salary}}(\pi_{\text{Name, Salary}}(\text{Employee}))$$
- **Explanation:** The `AS` keyword in SQL is used to rename a column or table with an alias. 
- In this query, the `Name` column is renamed to `EmployeeName` and the `Salary` column is renamed to `EmployeeSalary`. 
- In relational algebra, the $\rho$ operator is used for renaming.
---
## Pattern Matching (LIKE)

```sql
SELECT * 
FROM Employee 
WHERE Name LIKE 'J%';
```

$$\sigma_{\text{Name LIKE 'J\%'}}(Employee)$$
- **Explanation:** The `LIKE` operator in SQL is used for pattern matching. 
- In the given query, it retrieves data from the `Employee` table where the `Name` starts with 'J'. 
- The '%' represents zero, one, or multiple characters, while '\_' represents a single character in SQL's LIKE operator.
---

## Insertion

```sql
INSERT INTO Employee (Name, Age, Salary) 
	VALUES ('John Doe', 25, 50000);
```

$$\text{Employee} \leftarrow 
\pi_{
	\text{Name, Age, Salary}
}
(
	(\sigma_{\text{Name} \neq 
	'\text{John Doe}'}(\text{Employee})
) \cup 
(
('\text{John Doe}', 25, 55000)))$$
