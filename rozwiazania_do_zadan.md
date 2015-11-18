# Rozwiazania do zadań

## Instrukcja SELECT

Zadanie 1.1:

```
select employee_id, job_id, department_id
from job_history;
```

Rezultat:

EMPLOYEE_ID|JOB_ID|DEPARTMENT_ID
-- | --
102|IT_PROG|60
101|AC_ACCOUNT|110
101|AC_MGR|110
201|MK_REP|20
114|ST_CLERK|50
122|ST_CLERK|50
200|AD_ASST|90
176|SA_REP|80
176|SA_MAN|80
200|AC_ACCOUNT|90

Zadanie 1.2:

```
select *
from jobs;
```

JOB_ID|JOB_TITLE|MIN_SALARY|MAX_SALARY
 -- | -- | -- | -- | -- 
AD_PRES|President|20080|40000
AD_VP|Administration Vice President|15000|30000
AD_ASST|Administration Assistant|3000|6000
FI_MGR|Finance Manager|8200|16000
FI_ACCOUNT|Accountant|4200|9000
AC_MGR|Accounting Manager|8200|16000
AC_ACCOUNT|Public Accountant|4200|9000
SA_MAN|Sales Manager|10000|20080
SA_REP|Sales Representative|6000|12008
PU_MAN|Purchasing Manager|8000|15000
PU_CLERK|Purchasing Clerk|2500|5500
ST_MAN|Stock Manager|5500|8500
ST_CLERK|Stock Clerk|2008|5000
SH_CLERK|Shipping Clerk|2500|5500
IT_PROG|Programmer|4000|10000
MK_MAN|Marketing Manager|9000|15000
MK_REP|Marketing Representative|4000|9000
HR_REP|Human Resources Representative|4000|9000
PR_REP|Public Relations Representative|4500|10500
