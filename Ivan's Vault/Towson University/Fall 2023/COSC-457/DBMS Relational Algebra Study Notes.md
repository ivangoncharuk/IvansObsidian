---
tags:
  - COSC-457
  - fall2023
---

This was used to do [[DBMS Assignment 3]]

### 1. Selection Operation ($\sigma$)
- **Description**: Filters rows based on a condition.
- **Symbol**: $\sigma$
- **SQL Equivalent**: `WHERE`
- **Python Equivalent**: `.query()` or boolean indexing
- **Example**: 
  - Algebra: $\sigma_{Plocation = 'Houston'}(P)$
  - SQL: `SELECT * FROM P WHERE Plocation = 'Houston'`
  - Python: `P.query("Plocation == 'Houston'")`

### 2. Projection Operation ($\pi$)
- **Description**: Selects columns.
- **Symbol**: $\pi$
- **SQL Equivalent**: `SELECT <columns>`
- **Python Equivalent**: `[<columns>]`
- **Example**: 
  - Algebra: $\pi_{Fname, Lname}(E)$
  - SQL: `SELECT Fname, Lname FROM E`
  - Python: `E[['Fname', 'Lname']]`

### 3. Join Operation ($\bowtie$)
- **Description**: Combines rows based on a related column.
- **Symbol**: $\bowtie$
- **SQL Equivalent**: `JOIN...ON`
- **Python Equivalent**: `.merge(on=<column>)`
- **Example**: 
  - Algebra: $E \bowtie D$
  - SQL: `SELECT * FROM E JOIN D ON E.Dno = D.Dnumber`
  - Python: `E.merge(D, left_on='Dno', right_on='Dnumber')`

### 4. Grouping and Aggregation Operation 
- **Description**: Groups data and performs an operation on the grouped data.
- **Symbol**: (No specific symbol in relational algebra)
- **SQL Equivalent**: `GROUP BY` and aggregation functions like `AVG`, `SUM`, etc.
- **Python Equivalent**: `.groupby(<columns>).agg(<operation>)`
- **Example**: 
  - Algebra: No direct equivalent
  - SQL: `SELECT Dname, AVG(Salary) FROM E GROUP BY Dname`
  - Python: `E.groupby('Dname')['Salary'].mean()`

### 5. Difference Operation (-)
- **Description**: Retrieves rows from the first table that don't have corresponding rows in the second table.
- **Symbol**: -
- **SQL Equivalent**: `EXCEPT`
- **Python Equivalent**: `.merge(..., how='outer', indicator=True).query("_merge == 'left_only'")`
- **Example**: 
  - Algebra: $E - D$
  - SQL: No direct equivalent in standard SQL
  - Python: 
    ```python
    E.merge(D, how='outer', indicator=True)
      .query("_merge == 'left_only'")
    ```

### 6. Intersection Operation ($\cap$)
- **Description**: Retrieves rows common to both tables.
- **Symbol**: $\cap$
- **SQL Equivalent**: `INTERSECT`
- **Python Equivalent**: `.merge(on=<common_columns>)`
- **Example**: 
  - Algebra: $E \cap D$
  - SQL: `SELECT * FROM E INTERSECT SELECT * FROM D`
  - Python: `pd.merge(E, D)`

### 7. Division Operation
- **Description**: Identifies common values across related tables.
- **Symbol**: (No specific symbol in relational algebra)
- **SQL Equivalent**: Multiple nested `NOT EXISTS` clauses or similar subqueries.
- **Python Equivalent**: Various, depending on exact need – often a combination of `.groupby` and `.filter`.
- **Example**: 
  - Algebra: No direct equivalent
  - SQL: See the detailed query in the previous messages.
  - Python: Often involves using `.groupby` and `.filter`.

### 8. Union Operation ($\cup$)
- **Description**: Combines the rows of two tables (must have the same schema).
- **Symbol**: $\cup$
- **SQL Equivalent**: `UNION`
- **Python Equivalent**: `.concat()` or `.append()`
- **Example**: 
  - Algebra: $E \cup D$
  - SQL: `SELECT * FROM E UNION SELECT * FROM D`
  - Python: `pd.concat([E, D])` or `E.append(D)`

These operations form the foundation of relational algebra, which is the theoretical basis of SQL and data manipulation in relational databases. Each operation manipulates one or two relations and produces a relation as a result. This allows you to chain operations together to perform complex data retrieval and manipulation tasks.