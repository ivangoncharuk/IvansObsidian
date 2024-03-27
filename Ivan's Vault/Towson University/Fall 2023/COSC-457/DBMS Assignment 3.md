- Name: `Ivan Goncharuk`

![[DBMS_a3_supplier_part_table.png]]


# Problem 1
Basic Concepts (50 pts)
 1. Can we execute Supplier $\cup$ Part? And please justify your answer.
 - Ans - This operation is **not valid**. The union operation requires both relations (tables) to have the same attributes, which is not the case here. "Supplier" and "Part" have different attributes (SupplName, PartNumber vs. PartNumber, PartName).
 - Why - The union operator $\cup$ combines two sets to create a new set that is the result of combining the elements of both of the original sets.

Python code for 2 and 3:

```python
import pandas as pd

supplier = pd.DataFrame({
    'SupplName': ['Acme Inc.', 'Main St. Hardware', 'Electronics 2000'],
    'PartNumber': ['P120', 'N30', 'PM130']
})

part = pd.DataFrame({
    'PartNumber': ['N30', 'KCL12', 'P120'],
    'PartName': ['10" screw', '21b hammer', '10-ohm resistor']
})

# Supplier X Part
cartesian_product = pd.merge(supplier.assign(key=1), part.assign(key=1), on='key', suffixes=('', '_y')).drop('key', axis=1)

# σ (Supplier.PartNumber = Part.PartNumber) (Supplier X Part)
selected_rows = cartesian_product[cartesian_product['PartNumber'] == cartesian_product['PartNumber_y']]

(cartesian_product, selected_rows)

```


2.  Please execute Supplier X Part and show the result table.

The Cartesian product of two sets is a new set that contains all of the possible pairs of elements from the two original sets.

| SupplName         | PartNumber | PartNumber_y | PartName        |
| ----------------- | ---------- | ------------ | --------------- |
| Acme Inc.         | P120       | N30          | 10" screw       |
| Acme Inc.         | P120       | KCL12        | 21b hammer      |
| Acme Inc.         | P120       | P120         | 10-ohm resistor |
| Main St. Hardware | N30        | N30          | 10" screw       |
| Main St. Hardware | N30        | KCL12        | 21b hammer      |
| Main St. Hardware | N30        | P120         | 10-ohm resistor |
| Electronics 2000  | PM130      | N30          | 10" screw       |
| Electronics 2000  | PM130      | KCL12        | 21b hammer      |
| Electronics 2000  | PM130      | P120         | 10-ohm resistor |


3. Execute $\sigma_{\text{Supplier.PartNumber = Part.PartNumber}}$ (Supplier X Part)

| SupplName         | PartNumber | PartNumber_y | PartName        |
| ----------------- | ---------- | ------------ | --------------- |
| Acme Inc.         | P120       | P120         | 10-ohm resistor |
| Main St. Hardware | N30        | N30          | 10" screw       |

# Problem 2

**EMPLOYEE**: Specify relational algebra expressions for the following descriptions on the database schema shown in Figure 5.6 using the relational operators discussed in this chapter. Also show the results of each query using the above database tables. (50 points)

![[Employee_schema.png]]

Schema:

1. **EMPLOYEE**
    - Fname
    - Minit
    - Lname
    - Ssn
    - Bdate
    - Address
    - Sex
    - Salary
    - Super_ssn
    - Dno
2. **DEPARTMENT**
    - Dname
    - Dnumber
    - Mgr_ssn
    - Mgr_start_date
3. **DEPT_LOCATIONS**
    - Dnumber
    - Dlocation
4. **WORKS_ON**
    - Essn
    - Pno
    - Hours
5. **PROJECT**
    - Pname
    - Pnumber
    - Plocation
    - Dnum
6. **DEPENDENT**
    - Essn
    - Dependent_name
    - Sex
    - Bdate
    - Relationship

Tables:

| Fname    | Minit | Lname   | Ssn       | Bdate     | Address                 | Sex | Salary | Super_ssn | Dno |
|----------|-------|---------|-----------|-----------|-------------------------|-----|--------|-----------|-----|
| John     | B     | Smith   | 123456789 | 1965-01-09| 731 Fondren, Houston, TX| M   | 30000  | 333445555 | 5   |
| Franklin | T     | Wong    | 333445555 | 1955-12-08| 638 Voss, Houston, TX   | M   | 40000  | 888665555 | 5   |
| Alicia   | J     | Zelaya  | 999887777 | 1968-01-19| 3321 Castle, Spring, TX | F   | 25000  | 987654321 | 4   |
| Jennifer | S     | Wallace | 987654321 | 1941-06-20| 291 Berry, Bellaire, TX | F   | 43000  | 888665555 | 4   |
| Ramesh   | K     | Narayan | 666884444 | 1962-09-15| 975 Fire Oak, Humble, TX| M   | 38000  | 333445555 | 5   |
| Joyce    | A     | English | 453453453 | 1972-07-31| 5631 Rice, Houston, TX  | F   | 25000  | 333445555 | 5   |
| Ahmad    | V     | Jabbar  | 987987987 | 1969-03-29| 980 Dallas, Houston, TX | M   | 25000  | 987654321 | 4   |
| James    | E     | Borg    | 888665555 | 1937-11-10| 450 Stone, Houston, TX  | M   | 55000  | NULL      | 1   |

### DEPARTMENT

| Dname          | Dnumber | Mgr_ssn   | Mgr_start_date |
|----------------|---------|-----------|----------------|
| Research       | 5       | 333445555 | 1988-05-22     |
| Administration | 4       | 987654321 | 1995-01-01     |
| Headquarters   | 1       | 888665555 | 1981-06-19     |

### DEPT_LOCATIONS

| Dnumber | Dlocation |
|---------|-----------|
| 1       | Houston   |
| 4       | Stafford  |
| 5       | Bellaire  |
| 5       | Sugarland |
| 5       | Houston   |

### WORKS_ON

| Essn      | Pno | Hours |
|-----------|-----|-------|
| 123456789 | 1   | 32.5  |
| 123456789 | 2   | 7.5   |
| 666884444 | 3   | 40.0  |
| 453453453 | 1   | 20.0  |
| 453453453 | 2   | 20.0  |
| 333445555 | 2   | 10.0  |
| 333445555 | 3   | 10.0  |
| 333445555 | 10  | 10.0  |
| 999887777 | 30  | 30.0  |
| 987987987 | 10  | 35.0  |
| 987987987 | 30  | 5.0   |
| 987654321 | 30  | 20.0  |
| 987654321 | 20  | 15.0  |

### PROJECT

| Pname            | Pnumber | Plocation | Dnum |
|------------------|---------|-----------|------|
| ProductX         | 1       | Bellaire  | 5    |
| ProductY         | 2       | Sugarland | 5    |
| ProductZ         | 3       | Houston   | 5    |
| Computerization  | 10      | Stafford  | 4    |
| Reorganization   | 20      | Houston   | 1    |
| Newbenefits      | 30      | Stafford  | 4    |

### DEPENDENT

| Essn      | Dependent_name | Sex | Bdate     | Relationship |
|-----------|----------------|-----|-----------|--------------|
| 333445555 | Alice          | F   | 1986-04-05| Daughter     |
| 333445555 | Theodore       | M   | 1983-10-25| Son          |
| 333445555 | Joy            | F   | 1958-05-03| Spouse       |
| 987654321 | Abner          | M   | 1942-02-28| Spouse       |
| 123456789 | Michael        | M   | 1988-01-04| Son          |
| 123456789 | Alice          | F   | 1988-12-30| Daughter     |
| 123456789 | Elizabeth      | F   | 1967-05-05| Spouse       |

NOTE: I removed all instances where I manually entered in the table data in the python code blocks in this document so that the rendered pdf isn't as lengthy. I used the data above. 

a. Retrieve the names of employees in department 5 who work more than 10 hours per week on the 'ProductY' project.

Python:
```python
import pandas as pd

employee = pd.DataFrame(employee_data)

works_on = pd.DataFrame(works_on_data)


project_data = {
    'Pname': ['ProductX', 'ProductY', 'ProductZ', 'Computerization', 'Reorganization', 'Newbenefits'],
    'Pnumber': [1, 2, 3, 10, 20, 30]
}

project = pd.DataFrame(project_data)


result = (
    employee.merge(works_on, left_on='Ssn', right_on='Essn')
    .merge(project, left_on='Pno', right_on='Pnumber')
    .query("Dno == 5 & Pname == 'ProductY' & Hours > 10")[['Fname', 'Minit', 'Lname']]
)

result

```

result:

| Fname | Minit | Lname  |
|-------|-------|--------|
| Joyce | A     | English|

b. List the names of employees who have a dependent with the same first name as themselves.

SQL:
```SQL
SELECT Fname, Minit, Lname
FROM EMPLOYEE, DEPENDENT
WHERE EMPLOYEE.Ssn = DEPENDENT.Essn AND
      EMPLOYEE.Fname = DEPENDENT.Dependent_name;
```

Python:
```python

dependent = pd.DataFrame(dependent_data)

same_name_result = (
    employee.merge(dependent, left_on='Ssn', right_on='Essn')
    .query("Fname == Dependent_name")[['Fname', 'Minit', 'Lname']]
)

same_name_result

```

same_name_result:

```
Empty DataFrame
Columns: [Fname, Minit, Lname]
Index: []
```

c. Find the names of employees that are directly supervised by 'Franklin Wong'.

SQL:

```SQL
SELECT E.Fname, E.Minit, E.Lname
FROM EMPLOYEE E, EMPLOYEE S
WHERE E.Super_ssn = S.Ssn AND
      S.Fname = 'Franklin' AND
      S.Lname = 'Wong';

```

Python:

```python

employee = pd.DataFrame(employee_data)

supervised_by_franklin = (
    employee.merge(employee, left_on='Super_ssn', right_on='Ssn', suffixes=('', '_supervisor'))
    .query("Fname_supervisor == 'Franklin' & Lname_supervisor == 'Wong'")[['Fname', 'Minit', 'Lname']]
)

supervised_by_franklin

```

supervised_by_franklin:

| Fname  | Minit | Lname  |
|--------|-------|--------|
| John   | B     | Smith  |
| Ramesh | K     | Narayan|
| Joyce  | A     | English|

d. For each project, list the project name and the total hours per week (by all employees) spent on that project.

SQL:
```SQL
SELECT Pname, SUM(Hours) as Total_Hours
FROM PROJECT, WORKS_ON
WHERE PROJECT.Pnumber = WORKS_ON.Pno
GROUP BY Pname;
```

Python:
```python
project_hours = (
    project.merge(works_on, left_on='Pnumber', right_on='Pno')
    .groupby('Pname')['Hours'].sum().reset_index()
    .rename(columns={'Hours': 'Total_Hours'})
)
project_hours

```

| Pname            | Total_Hours |
|------------------|-------------|
| Computerization  | 45.0        |
| Newbenefits      | 55.0        |
| ProductX         | 52.5        |
| ProductY         | 37.5        |
| ProductZ         | 50.0        |
| Reorganization   | 15.0        |


e. Retrieve the names of employees who work on every project (Hint: Division function can be used. You can create a Proj_Emp relation with attribute of Pno and SSN, which describe the work on relation between employee and project. Divide it by a Proj(Pno) relation).

SQL:
```SQL
SELECT E.Fname, E.Minit, E.Lname
FROM EMPLOYEE E
WHERE NOT EXISTS (
    SELECT P.Pnumber
    FROM PROJECT P
    WHERE NOT EXISTS (
        SELECT W.Essn
        FROM WORKS_ON W
        WHERE W.Pno = P.Pnumber AND W.Essn = E.Ssn
    )
);
```

Python:

```python

unique_projects = project['Pnumber'].unique()

all_project_employees = (
    works_on.groupby('Essn')
    .filter(lambda g: set(g['Pno'].unique()) >= set(unique_projects))
    ['Essn'].unique()
)

employee_every_project = employee[employee['Ssn'].isin(all_project_employees)][['Fname', 'Minit', 'Lname']]

employee_every_project

```

employee_every_project:
```
Empty DataFrame
Columns: [Fname, Minit, Lname]
Index: []
```

f. Retrieve the names of employees who do not work on any project (Hint: Minus function can be used).

```python
no_project_employees = employee[
    ~employee['Ssn'].isin(works_on['Essn'].unique())
][['Fname', 'Minit', 'Lname']]

no_project_employees

```

no_project_employees:

| Fname | Minit | Lname |
|-------|-------|-------|
| James | E     | Borg  |

g. For each department, retrieve the department name, and the average salary of employees working in that department

SQL:

```SQL
SELECT D.Dname, AVG(E.Salary) as Avg_Salary
FROM DEPARTMENT D, EMPLOYEE E
WHERE E.Dno = D.Dnumber
GROUP BY D.Dname;
```

```python
department = pd.DataFrame(department_data)

avg_salary_per_dept = (
    employee.merge(department, left_on='Dno', right_on='Dnumber')
    .groupby('Dname')['Salary'].mean().reset_index()
    .rename(columns={'Salary': 'Avg_Salary'})
)

avg_salary_per_dept
```

avg_salary_per_dept:

| Dname          | Avg_Salary |
|----------------|------------|
| Administration | 31000.0    |
| Headquarters   | 55000.0    |
| Research       | 33250.0    |

h. Retrieve the average salary of all female employees.

SQL:
```SQL
SELECT AVG(Salary) as Avg_Salary
FROM EMPLOYEE
WHERE Sex = 'F';
```

Python:
```python
avg_salary_female = employee[employee['Sex'] == 'F']['Salary'].mean()

avg_salary_female
```

avg_salary_female:
```
31000.0
```


Denoting...
- $E$ as the `EMPLOYEE` table,
- $P$ as the `PROJECT` table,
- $D$ as the `DEPARTMENT` table,
- $W$ as the `WORKS_ON` table,
- $L$ as the `DEPT_LOCATIONS` table.

Select Operation:
$$
\begin{align*}
P_{\text{Houston}}​&=\sigma_{\text{Plocation =′Houston′}​}(P) \\
L_{\text{Houston}}&=\sigma_{\text{Dlocation=′Houston′}​}(L)
\end{align*}
$$

Join Operation:
$$EP_{Houston}​=E \bowtie (W \bowtie P{Houston}​)$$

Join and Different Operation:
$$EP_{\text{not Houston}}​ = E \bowtie (D - (D \bowtie L_\text{Houston}))$$

Difference Operation:
$$E_{\text{Result}} = EP_{\text{Houston}} - E_{\text{not Houston}}$$

Project Operation:
$$\pi_{F_{\text{name}}, M_{\text{init}}, L_{\text{name}}, \text{Address}}(E_{\text{Result}})$$

Python:
```python

project = pd.DataFrame(project_data)

# 1. Selection Operation
P_Houston = project.query("Plocation == 'Houston'")
L_Houston = dept_locations.query("Dlocation == 'Houston'")

# 2. Join Operation: Employees working on projects in Houston
EP_Houston = employee.merge(
    works_on.merge(P_Houston, left_on='Pno', right_on='Pnumber'),
    left_on='Ssn', right_on='Essn'
)

# 3. Join and Difference Operation: Employees whose department has no location in Houston
E_not_Houston = employee.merge(
    department[~department['Dnumber'].isin(L_Houston['Dnumber'])],
    left_on='Dno', right_on='Dnumber'
)

# 4. Difference Operation
E_Result = EP_Houston.merge(
    E_not_Houston, 
    on=['Fname', 'Minit', 'Lname', 'Ssn', 'Bdate', 'Address', 'Sex', 'Salary', 'Super_ssn', 'Dno'],
    how='outer', 
    indicator=True
).query("_merge == 'left_only'")

# 5. Projection Operation
result_employees = E_Result[['Fname', 'Minit', 'Lname', 'Address']]

result_employees

```

result_employees:

| Fname    | Minit | Lname    | Address                 |
|----------|-------|----------|-------------------------|
| Franklin | T     | Wong     | 638 Voss, Houston, TX   |
| Ramesh   | K     | Narayan  | 975 Fire Oak, Humble, TX|

j.  List the last names of department managers who have dependent(s). (Hint: Intersection of manager and employee with dependents.

SQL:
```SQL
SELECT DISTINCT M.Lname
FROM EMPLOYEE M, DEPARTMENT D, DEPENDENT DE
WHERE M.Ssn = D.Mgr_ssn AND M.Ssn = DE.Essn;
```

Python:
```python
MD = pd.merge(M, ED, on=['Ssn'], how='inner', suffixes=('_M', '_ED'))[['Lname_M']].rename(columns={'Lname_M': 'Lname'})

MD
```

MD:

| Lname  |
|--------|
| Wong   |
| Wallace|
