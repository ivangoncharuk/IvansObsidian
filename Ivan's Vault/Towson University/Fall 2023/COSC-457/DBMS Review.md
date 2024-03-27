

$$
\pi_{\text{Fname}, \text{Lname}}(
  (\sigma_{\text{Dno} = 5}(
    \text{EMPLOYEE})
  )
  \bowtie
  (\sigma_{\text{Hours} > 10}(
    (\pi_{\text{Pnumber}}(
      \sigma_{\text{Pname} = \text{'ProductY'}}(\text{PROJECT})
    ))
    \bowtie
    \text{WORKS\_ON}
  ))
)
$$
```SQL
SELECT E.Fname, E.Lname
FROM EMPLOYEE E, PROJECT P, WORKS_ON W
WHERE E.Ssn = W.Essn
  AND W.Pno = P.Pnumber
  AND P.Pname = 'ProductY'
  AND W.Hours > 10
  AND E.Dno = 5;
```

| Relational Algebra                    | SQL                                             |
| ------------------------------------- | ----------------------------------------------- |
| Fname, Lname                          | SELECT E.Fname, E.Lname                         |
| Conditions                            | WHERE clause with the conditions                |
| EMPLOYEE                              | FROM EMPLOYEE E                                 |
| PROJECT                               | FROM PROJECT P                                  |
| WORKS_ON                              | FROM WORKS_ON W                                 |
| ⋈                                     | Implicit join condition within the WHERE clause |
| Pname = 'ProductY' (PROJECT)          | (PROJECT)                                       |
| $\sigma$ Pname = 'ProductY' (PROJECT) | AND P.Pname = 'ProductY'                        |
| $\sigma${Hours > 10}(WORKS_ON)        | AND W.Hours > 10                                |
| Dno = 5 (EMPLOYEE)                    | (EMPLOYEE)                                      |
| σ Dno = 5 (EMPLOYEE)                  | AND E.Dno = 5                                   |
