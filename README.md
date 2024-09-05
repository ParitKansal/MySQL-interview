# MySQL-interview


### LIKE
- The percent sign (%) represents zero, one, or multiple characters
- The underscore sign (_) represents one, single character


### REGEXP
```
SELECT user_id, name, mail
FROM Users
WHERE mail REGEXP '^[a-zA-Z]{1}[a-zA-Z0-9\\_\\.\\-]*\\@leetcode\\.com$';
```


### CASE
```sql
SELECT CASE 
    WHEN gender="M" 
        THEN "Male"
    WHEN gender="F" 
        THEN "Female"
    ELESE 
        "Others"
    END AS gender
FROM employee;
```


### Aggregate Function

#### DATE_FORMAT()
```mysql
SELECT DATE_FORMAT(<column>, '%d-%m-%Y') AS date_value
```
- %M	Month name in full (January to December)
- %m	Month name as a numeric value (00 to 12)
- %Y	Year as a numeric, 4-digit value
- %y	Year as a numeric, 2-digit value
- %d	Day of the month as a numeric value (01 to 31)

#### INSTR(str,substr) -> index = 1
Returns the position of the first occurrence of substring substr in string str.

####  SUBSTRING(str,pos,len)-> index = 1

#### CAST(<exp> AS DECIMAL)
DECIAML / FLOAT / CHAR


### WITH Clause
```sql
WITH table1 (col1, col2) AS
(
    -- query1
),
table2 (col1, col2) AS
(
    -- query2
)

SELECT *
FROM table1
JOIN table2 ON table1.col1 = table2.col1;
```

**WRONG**
```
WITH table1 (avg_salary) AS
(
    SELECT AVG(salary) FROM employee
)
SELECT * 
FROM employee 
WHERE salary > table1.avg_salary;
```

**Right**
```
WITH table1 (avg_salary) AS
(
    SELECT AVG(salary) FROM employee
)
SELECT * 
FROM employee 
WHERE salary > (SELECT avg_salary FROM table1);
```

```
WITH table1 (avg_salary) AS
(
    SELECT AVG(salary) FROM employee
)
SELECT e.* 
FROM employee e
CROSS JOIN table1
WHERE e.salary > table1.avg_salary;
```
