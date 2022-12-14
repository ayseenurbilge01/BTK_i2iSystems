# Q1
```sql
SELECT EMPLOYEE_ID, FIRST_NAME, DEPARTMENT_NAME 
FROM HR.EMPLOYEES emp JOIN HR.DEPARTMENTS dep
ON emp.EMPLOYEE_ID = dep.DEPARTMENT_ID
```
# Q2
```sql
SELECT  m.EMPLOYEE_ID, e.EMPLOYEE_ID "MANAGER_ID"
FROM HR.EMPLOYEES e JOIN HR.EMPLOYEES m 
ON (e.EMPLOYEE_ID = m.MANAGER_ID)
```
# Q3
```sql
SELECT SUBSTR(PHONE_NUMBER,1,3) "Operator",COUNT(PHONE_NUMBER) "Total" FROM HR.EMPLOYEES GROUP BY SUBSTR(PHONE_NUMBER,1,3)

WITH QUERY AS
(
SELECT SUBSTR(PHONE_NUMBER,1,3) "Operator" ,COUNT(PHONE_NUMBER) "Total"
FROM HR.EMPLOYEES 
GROUP BY SUBSTR(PHONE_NUMBER,1,3))
SELECT *
FROM QUERY
PIVOT
(
SUM("Total") FOR "Operator"  IN (011,515,650,603,590)
)
```
# Q4
```sql
DESCRIBE HR.EMPLOYEES

CREATE TABLE EMP   
(
    EMPLOYEE_ID NUMBER(6,0) NOT NULL,
    FIRST_NAME VARCHAR2(20),
    LAST_NAME VARCHAR2(25) NOT NULL,
    EMAIL VARCHAR2(25) NOT NULL,
    PHONE_NUMBER VARCHAR2(20),
    HIRE_DATE DATE NOT NULL,
    JOB_ID VARCHAR2(10) NOT NULL,
    SALARY NUMBER(8,2),
    COMMISSION_PCT NUMBER(2,2),
    MANAGER_ID NUMBER(6,0),
    DEPARTMENT_ID NUMBER(4,0),
    PRIMARY KEY(EMPLOYEE_ID)
)

INSERT INTO EMP(EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,MANAGER_ID,DEPARTMENT_ID)
SELECT EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,MANAGER_ID,DEPARTMENT_ID
FROM HR.EMPLOYEES

SELECT * FROM EMP

INSERT INTO EMP(EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,HIRE_DATE,JOB_ID,SALARY,MANAGER_ID,DEPARTMENT_ID)
VALUES(15000,'Ayşe','Nur','aysenurbilge01@gmail.com','17-JUN-03','IT_PROG',15000,103,60)

UPDATE EMP SET PHONE_NUMBER=5520895580,SALARY=20000 WHERE EMPLOYEE_ID=15000

SELECT * FROM EMP WHERE EMPLOYEE_ID=15000

DELETE FROM EMP WHERE EMPLOYEE_ID=15000

DROP TABLE EMP
```
# Q5
```sql
SELECT RPAD(REGEXP_REPLACE(FIRST_NAME,'(\w{2})\w+','\1'),LENGTH(FIRST_NAME),'*')||' '||RPAD(REGEXP_REPLACE(FIRST_NAME,'(\w{2})\w+','\1'),LENGTH(LAST_NAME),'*') as EMPLOYEENAME FROM HR.EMPLOYEES
```
