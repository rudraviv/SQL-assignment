HR Database 

1 . Display department name and manager first name .
```sql
mysql> SELECT d.DEPARTMENT_NAME,e.FIRST_NAME FROM departments d INNER JOIN employees e ON d.MANAGER_ID=e.MANAGER_ID LIMIT 10;
+-----------------+------------+
| DEPARTMENT_NAME | FIRST_NAME |
+-----------------+------------+
| Marketing       | Pat        |
| Purchasing      | Alexander  |
| Purchasing      | Shelli     |
| Purchasing      | Sigal      |
| Purchasing      | Guy        |
| Purchasing      | Karen      |
| Shipping        | Laura      |
| Shipping        | Mozhe      |
| Shipping        | James      |
| Shipping        | TJ         |
+-----------------+------------+
10 rows in set (0.00 sec)
```
2 . Display department name , manager name , and city .
```sql
mysql> SELECT d.DEPARTMENT_NAME,e.FIRST_NAME,l.CITY FROM departments d INNER JOIN locations l ON d.LOCATION_ID=l.LOCATION_ID INNER JOIN employees e ON d.MANAGER_ID=e.MANAGER_ID LIMIT 10;
+-----------------+------------+---------------------+
| DEPARTMENT_NAME | FIRST_NAME | CITY                |
+-----------------+------------+---------------------+
| Marketing       | Pat        | Toronto             |
| Purchasing      | Alexander  | Seattle             |
| Purchasing      | Shelli     | Seattle             |
| Purchasing      | Sigal      | Seattle             |
| Purchasing      | Guy        | Seattle             |
| Purchasing      | Karen      | Seattle             |
| Shipping        | Laura      | South San Francisco |
| Shipping        | Mozhe      | South San Francisco |
| Shipping        | James      | South San Francisco |
| Shipping        | TJ         | South San Francisco |
+-----------------+------------+---------------------+
10 rows in set (0.00 sec)

```
3 . Display country name , city , and department name .
'''sql
mysql> SELECT d.DEPARTMENT_NAME,l.CITY,c.COUNTRY_NAME FROM countries c INNER JOIN locations l ON c.COUNTRY_ID=l.COUNTRY_ID  INNER JOIN departments d ON d.LOCATION_ID=l.LOCATION_ID LIMIT 10;
+------------------+---------------------+--------------------------+
| DEPARTMENT_NAME  | CITY                | COUNTRY_NAME             |
+------------------+---------------------+--------------------------+
| Administration   | Seattle             | United States of America |
| Marketing        | Toronto             | Canada                   |
| Purchasing       | Seattle             | United States of America |
| Human Resources  | London              | United Kingdom           |
| Shipping         | South San Francisco | United States of America |
| IT               | Southlake           | United States of America |
| Public Relations | Munich              | Germany                  |
| Executive        | Seattle             | United States of America |
| Finance          | Seattle             | United States of America |
| Accounting       | Seattle             | United States of America |
+------------------+---------------------+--------------------------+
10 rows in set (0.00 sec)

'''

4 . Display job title , department name , employee last name ,
starting date for all jobs from 2000 to 2005 .
```sql
SELECT 
```
5 . Display job title and average salary of employees
```SQL
mysql> SELECT j.JOB_TITLE,AVG(e.SALARY) FROM jobs j INNER JOIN employees e ON j.JOB_ID=e.JOB_ID GROUP BY j.JOB_TITLE LIMIT 10;
+-------------------------------+---------------+
| JOB_TITLE                     | AVG(e.SALARY) |
+-------------------------------+---------------+
| President                     |  24000.000000 |
| Administration Vice President |  17000.000000 |
| Administration Assistant      |   4400.000000 |
| Finance Manager               |  12000.000000 |
| Accountant                    |   7920.000000 |
| Accounting Manager            |  12000.000000 |
| Public Accountant             |   8300.000000 |
| Sales Manager                 |  12200.000000 |
| Sales Representative          |   8350.000000 |
| Purchasing Manager            |  11000.000000 |
+-------------------------------+---------------+
10 rows in set (0.01 sec)
```

6 . Display job title , employee name , and the difference
between maximum salary for the job and salary of the
employee .SELECT * FROM jobs INNER JOIN employees ON employees.JOB_ID=jobs.JOB_ID WHERE employees.SALARY>15000;

```SQL
mysql> SELECT j.JOB_TITLE,e.FIRST_NAME,j.MAX_SALARY-e.SALARY AS "DIFF"FROM jobs j INNER JOIN employees e ON j.JOB_ID=e.JOB_ID LIMIT 10;
+-------------------------------+-------------+----------+
| JOB_TITLE                     | FIRST_NAME  | DIFF     |
+-------------------------------+-------------+----------+
| President                     | Steven      | 16000.00 |
| Administration Vice President | Neena       | 13000.00 |
| Administration Vice President | Lex         | 13000.00 |
| Administration Assistant      | Jennifer    |  1600.00 |
| Finance Manager               | Nancy       |  4000.00 |
| Accountant                    | Daniel      |     0.00 |
| Accountant                    | John        |   800.00 |
| Accountant                    | Ismael      |  1300.00 |
| Accountant                    | Jose Manuel |  1200.00 |
| Accountant                    | Luis        |  2100.00 |
+-------------------------------+-------------+----------+
10 rows in set (0.00 sec)

```

7 . Display last name , job title of employees who have
commission percentage and belongs to department 30.

```SQL
mysql> SELECT e.LAST_NAME,j.JOB_TITLE FROM jobs j INNER JOIN employees e ON e.JOB_ID=j.JOB_ID WHERE COMMISSION_PCT is NOT NULL AND DEPARTMENT_ID=30;
+------------+--------------------+
| LAST_NAME  | JOB_TITLE          |
+------------+--------------------+
| Raphaely   | Purchasing Manager |
| Khoo       | Purchasing Clerk   |
| Baida      | Purchasing Clerk   |
| Tobias     | Purchasing Clerk   |
| Himuro     | Purchasing Clerk   |
| Colmenares | Purchasing Clerk   |
+------------+--------------------+
6 rows in set (0.00 sec)

```


8 . Display details of jobs that were done by any employee who
is currently drawing more than 15000 of salary .
```sql
mysql> SELECT jobs.JOB_ID,jobs.JOB_TITLE,jobs.MIN_SALARY,jobs.MAX_SALARY FROM jobs  INNER JOIN employees ON employees.JOB_ID=jobs.JOB_ID WHERE employees.SALARY>15000 LIMIT 10;
+---------+-------------------------------+------------+------------+
| JOB_ID  | JOB_TITLE                     | MIN_SALARY | MAX_SALARY |
+---------+-------------------------------+------------+------------+
| AD_PRES | President                     |      20000 |      40000 |
| AD_VP   | Administration Vice President |      15000 |      30000 |
| AD_VP   | Administration Vice President |      15000 |      30000 |
+---------+-------------------------------+------------+------------+
3 rows in set (0.00 sec) 
```


9 . Display department name , manager name , and salary of the
manager for all managers whose experience is more than 5
years .

```sql
mysql> SELECT d.DEPARTMENT_NAME,e.FIRST_NAME,e.SALARY FROM departments d INNER JOIN employees e ON(d.MANAGER_ID=e.EMPLOYEE_ID)WHERE DATEDIFF(SYSDATE(),e.HIRE_DATE)/365 > 5 ;
+------------------+------------+----------+
| DEPARTMENT_NAME  | FIRST_NAME | SALARY   |
+------------------+------------+----------+
| Administration   | Jennifer   |  4400.00 |
| Marketing        | Michael    | 13000.00 |
| Purchasing       | Den        | 11000.00 |
| Human Resources  | Susan      |  6500.00 |
| Shipping         | Adam       |  8200.00 |
| IT               | Alexander  |  9000.00 |
| Public Relations | Hermann    | 10000.00 |
| Sales            | John       | 14000.00 |
| Executive        | Steven     | 24000.00 |
| Finance          | Nancy      | 12000.00 |
| Accounting       | Shelley    | 12000.00 |
+------------------+------------+----------+
11 rows in set (0.00 sec)

```

10 . Display employee name if the employee joined before his
manager .
```SQL
mysql> SELECT e.FIRST_NAME FROM employees e INNER JOIN employees m on e.EMPLOYEE_ID = m.MANAGER_ID WHERE e.HIRE_DATE >m.HIRE_DATE;
Empty set (0.00 sec)
```
11 . Display employee name , job title for the jobs employee did
in the past where the job was done less than six months .

```sql
mysql> SELECT e.FIRST_NAME,j.JOB_TITLE,jh.START_DATE,jh.END_DATE FROM employees e INNER JOIN jobs j ON e.JOB_ID=j.JOB_ID INNER JOIN job_history jh ON j.JOB_ID=jh.JOB_ID WHERE DATEDIFF(END_DATE,START_DATE)/365<0.5;
Empty set (0.00 sec)
```
12 . Display employee name and country in which he is
working.
```SQL
SELECT e.FIRST_NAME,c.COUNTRY_NAME FROM employees e INNER JOIN departments d
ON e.DEPARTMENT_ID=d.DEPARTMENT_ID INNER JOIN locations l ON d.LOCATION_ID=l.LOCATION_ID INNER JOIN countries c ON l.COUNTRY_ID=c.COUNTRY_ID;  
```
13 . Display department name , average salary and number of
employees with commission within the department.
```SQL
mysql> select d.DEPARTMENT_NAME "Department Name",avg(e.salary)"Average Salary",count(e.EMPLOYEE_ID)"No. of Employees" from employees e inner join departments d on e.DEPARTMENT_ID=d.DEPARTMENT_ID where  e.COMMISSION_PCT !=0 group by d.DEPARTMENT_ID;
+-----------------+----------------+------------------+
| Department Name | Average Salary | No. of Employees |
+-----------------+----------------+------------------+
| Sales           |    8955.882353 |               34 |
+-----------------+----------------+------------------+
1 row in set (0.00 sec)
```
14 . Display the month in which more than 5 employees joined
in any department located in Sydney .
```SQL
SELECT COUNT(e.EMPLOYEE_ID)"count",MONTHNAME(e.HIRE_DATE)FROM employees e GROUP BY MONTHNAME(e.HIRE_DATE) HAVING COUNT(e.EMPLOYEE_ID)>5;

SELECT d.DEPARTMENT_NAME FROM departments d INNER JOIN locations l ON l.LOCATION_ID=d.DEPARTMENT_ID WHERE l.CITY="Sydney";


```

15 . Display details of departments in which the maximum salary
is more than 10000 .

16 . Display employee name , job title , start date , and end date
of past jobs of all employees with commission percentage null .

```SQL
SELECT e.EMPLOYEE_NAME,j.JOB_TITLE,jh.START_DATE,jh.END_DATE FROM 
```


SPJ Database



1 . Display the Supplier name and the Quantity sold .
```sql
SELECT S.Sname,sp.qty FROM S INNER JOIN sp ON S.`S#`=sp.`S#`;
```

2 . Display the Part name and Quantity sold .

```SQL
mysql> SELECT P.Pname,sp.qty FROM P INNER JOIN sp ON P.`P#`=sp.`P#`;
+-------+------+
| Pname | qty  |
+-------+------+
| Nut   |  200 |
| Nut   |  700 |
| Screw |  400 |
| Screw |  200 |
| Screw |  200 |
| Screw |  500 |
| Screw |  600 |
| Screw |  400 |
| Screw |  800 |
| Cam   |  100 |
| Screw |  200 |
| Screw |  500 |
| Cog   |  300 |
| Cog   |  300 |
+-------+------+
14 rows in set (0.00 sec)

```

3 . Display the Project name and Quantity sold .

mysql> SELECT J.Jname,sp.qty FROM J INNER JOIN sp ON J.`J#`=sp.`J#`;
+----------+------+
| Jname    | qty  |
+----------+------+
| Sorter   |  200 |
| Console  |  700 |
| Sorter   |  400 |
| Punch    |  200 |
| Reader   |  200 |
| Console  |  500 |
| Collator |  600 |
| Terminal |  400 |
| Tape     |  800 |
| Punch    |  100 |
| Sorter   |  200 |
| Punch    |  500 |
| Reader   |  300 |
| Tape     |  300 |
+----------+------+
14 rows in set (0.00 sec)


4 . Display the Supplier name , Part name , Project name and
Quantity sold .

```SQL
mysql> SELECT S.Sname,P.Pname,J.Jname,sp.qty FROM S INNER JOIN sp ON sp.`S#`=S.`S#` INNER JOIN P ON P.`P#`=sp.`P#` INNER JOIN J ON J.`J#`=sp.`J#`;
+-------+-------+----------+------+
| Sname | Pname | Jname    | qty  |
+-------+-------+----------+------+
| Smith | Nut   | Sorter   |  200 |
| Jones | Screw | Sorter   |  400 |
| Blake | Screw | Sorter   |  200 |
| Jones | Screw | Punch    |  200 |
| Blake | Screw | Punch    |  500 |
| Jones | Cam   | Punch    |  100 |
| Jones | Screw | Reader   |  200 |
| Clark | Cog   | Reader   |  300 |
| Smith | Nut   | Console  |  700 |
| Jones | Screw | Console  |  500 |
| Jones | Screw | Collator |  600 |
| Jones | Screw | Terminal |  400 |
| Jones | Screw | Tape     |  800 |
| Clark | Cog   | Tape     |  300 |
+-------+-------+----------+--
```

5 . Display the Supplier name , Supplying Parts to a Project in
the same City .

mysql> SELECT S.Sname,P.Pname FROM S INNER JOIN P ON S.City=P.CITY INNER JOIN J ON J.City = S.City;
+-------+-------+
| Sname | Pname |
+-------+-------+
| Jones | Bolt  |
| Blake | Bolt  |
| Jones | Cam   |
| Blake | Cam   |
| Smith | Nut   |
| Clark | Nut   |
| Smith | Screw |
| Clark | Screw |
| Smith | Cog   |
| Clark | Cog   |
| Smith | Nut   |
| Clark | Nut   |
| Smith | Screw |
| Clark | Screw |
| Smith | Cog   |
| Clark | Cog   |
+-------+-------+
16 rows in set (0.00 sec)


6 . Display the Part name that is ‘ Red ’ is color , and the
Quantity sold .

```SQL
mysql> SELECT P.Pname,P.Color,sp.qty from P INNER JOIN sp on P.`P#`=sp.`P#` WHERE P.Color="Red";
+-------+-------+------+
| Pname | Color | qty  |
+-------+-------+------+
| Nut   | Red   |  200 |
| Nut   | Red   |  700 |
| Screw | Red   |  500 |
| Cog   | Red   |  300 |
| Cog   | Red   |  300 |
+-------+-------+------+
5 rows in set (0.00 sec)
```
7 . Display all the Quantity sold by Suppliers with the Status =20 .
```SQL
mysql> SELECT S.Sname,S.Status,sp.qty FROM sp INNER JOIN S ON S.`S#`=sp.`S#` WHERE S.Status=20;
+-------+--------+------+
| Sname | Status | qty  |
+-------+--------+------+
| Smith |     20 |  200 |
| Smith |     20 |  700 |
| Clark |     20 |  300 |
| Clark |     20 |  300 |
+-------+--------+------+
4 rows in set (0.00 sec)
```
8 . Display all the Parts and Quantity with a Weight > 14 .

```SQL
mysql> SELECT P.Pname,sp.qty FROM P INNER JOIN sp ON P.`P#`=sp.`P#` WHERE P.Weight>14;
+-------+------+
| Pname | qty  |
+-------+------+
| Screw |  400 |
| Screw |  200 |
| Screw |  200 |
| Screw |  500 |
| Screw |  600 |
| Screw |  400 |
| Screw |  800 |
| Screw |  200 |
| Cog   |  300 |
| Cog   |  300 |
+-------+------+

```
9 . Display all the Project names and City , which has bought
more than 500 Parts .
```SQL
mysql>   SELECT  J.Jname,J.City FROM J INNER JOIN sp ON J.`J#`=sp.`J#` WHERE sp.qty>500;
+----------+--------+
| Jname    | City   |
+----------+--------+
| Console  | Athens |
| Collator | London |
| Tape     | London |
+----------+--------+
3 rows in set (0.00 sec)
```
10 . Display all the Part names and Quantity sold that have a
Weight less than 15 .

```SQL
mysql> SELECT P.Pname,sp.qty FROM P INNER JOIN sp ON P.`P#`=sp.`P#` WHERE P.Weight<15;
+-------+------+
| Pname | qty  |
+-------+------+
| Nut   |  200 |
| Nut   |  700 |
| Cam   |  100 |
| Screw |  500 |
+-------+------+
4 rows in set (0.00 sec)


```

11 . Display all the Suppliers with the same Status as the
supplier , ‘ CLARK ’.
```SQL
  mysql>   SELECT S.Sname,S.Status FROM S WHERE S.Sname!='Clark' AND S.Status=ALL(SELECT Status FROM S WHERE Sname='Clark');
+-------+--------+
| Sname | Status |
+-------+--------+
| Smith |     20 |
+-------+--------+
1 row in set (0.00 sec)


```

12 . Display all the Employees in the same department as the
employee ‘ MILLER ’.


13 . Display all the Parts which have more Weight than all the
Red parts .
```SQL
mysql> SELECT P1.Pname FROM P P1 INNER JOIN P P2 ON P1.`P#`=P2.`P#` WHERE P1.Weight>ALL(SELECT Weight FROM P WHERE Color = 'Red');
Empty set (0.00 sec)

```

14 . Display all the Projects going on in the same city as the
project ‘ TAPE ’.
```SQL
mysql> SELECT J1.Jname FROM J J1 INNER JOIN J J2 ON J1.`J#`=J2.`J#` WHERE J1.CITY=(SELECT CITY FROM J WHERE Jname='Tape')AND J1.Jname!='Tape';
+----------+
| Jname    |
+----------+
| Collator |
+----------+
1 row in set (0.00 sec)

```
15 . Display all the Parts with Weight less than all the Green
parts .
```SQL
mysql> SELECT P1.Pname,P1.Color FROM P P1 INNER JOIN P P2 ON P1.`P#`=P2.`P#`WHERE P1.Weight<ALL(SELECT Weight FROM P WHERE Color='Green');
+-------+-------+
| Pname | Color |
+-------+-------+
| Nut   | Red   |
| Screw | Red   |
| Cam   | Blue  |
+-------+-------+
3 rows in set (0.01 sec)
 
```

16 . Display the name of the Supplier who has sold the
maximum Quantity ( in onesale ).
```SQL
mysql> SELECT S.Sname,sp.qty FROM S INNER JOIN sp ON S.`S#`=sp.`S#`WHERE sp.qty=(SELECT MAX(qty)FROM sp );
+-------+------+
| Sname | qty  |
+-------+------+
| Jones |  800 |
+-------+------+
1 row in set (0.00 sec)
```
17 . Display the name of the Employee with the minimum
Salary .

```sql

```

18 . Display the name of the Supplier who has sold the
maximum overall Quantity ( sumof Sales ).

```SQL
SELECT S.Sname,sp.qty FROM S INNER JOIN sp ON S.`S#`=sp.`S#`WHERE sp.qty=(SELECT MAX(SUM(qty))FROM sp );
```

SALES DATABASE
1. Write a query that lists each order number followed by the
name of the customer who made the order .

```sql
select o.onum,c.cnum from ORDERS o inner join CUSTOMERS c on c.cnum=o.cnum;
```
2 . Write a query that gives the names of both the salesperson
and the customer for each order along with the order number .

```sql
SELECT c.name,o.onum,s.sname FROM CUSTOMERS c INNER JOIN ORDERS o ON c.cnum=o.cnum INNER JOIN SALESPEOPLE s ON o.snum=s.snum;
```
4 . Write a query that calculates the amount of the
salesperson ’ s commission on each order by a customer with a
rating above 100 .

```sql
SELECT c.cname,c.rating,s.num,s.sname,o.amt*s.comm AS commision FROM ORDERS o INNER JOIN CUSTOMERS c ON c.cnum=o.cnum INNER JOIN SALESPEOPLE s ON c.snum=s.snum WHERE c.rating >100;
```
SELECT d.DEPARTMENT_NAME,e.FIRST_NAME,e.SALARY FROM employees e INNER  JOIN departments d INNER JOIN job_history jh WHERE DATEDIFF(year,jh.END_DATE,jh.START_DATE);
5 . Write a query that produces all pairs of salespeople who are
living in the same city . Exclude combinations of salespeople with
themselves as well as duplicate rows with
the order reversed .

```sql
SELECT s1.sname,s1.city,s2.sname,s2.city FROM SALESPEOPLE s1  INNER JOIN SALESPEOPLE s2 ON s1.city=s2.city WHERE s1.sname>s2.sname;
```
6 . Write a query that produces the names and cities of all
customers with the same rating as Hoffman .
```sql
SELECT c1.name,c1.rating,c2.name,c2.rating FROM CUSTOMERS c1 INNER JOIN CUSTOMER c2 ON c1.cname=c2.cname WHERE c1.cname!='Hoffman' AND c2.cname='Hoffman';
```