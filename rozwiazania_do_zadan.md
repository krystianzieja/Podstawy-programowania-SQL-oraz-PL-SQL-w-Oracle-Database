# Rozwiazania do zadań

## Instrukcja SELECT

#### Zadanie 1.1

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

#### Zadanie 1.2:

```
select *
from jobs;
```

Alternatywne rozwiązanie polega na podanie wszystkich kolumn na liście select.

```
select job_id, job_title, min_salary, max_salary
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

#### Zadanie 1.3

```
select distinct department_id
from departments;
```

Rezultat:

| DEPARTMENT_ID |
| -- |
| 10 |
| 20 |
| 30 |
| 40 |
| 50 |
| 60 |
| 70 |
| 80 |
| 90 |
| 100 |
| 110 |
| 120 |
| 130 |
| 140 |
| 150 |
| 160 |
| 170 |
| 180 |
| 190 |
| 200 |
| 210 |
| 220 |
| 230 |
| 240 |
| 250 |
| 260 |
| 270 |

#### Zadanie 1.4

```
select distinct job_id, salary
from employees;
```

Rezultat:

JOB_ID|SALARY
-- | --
FI_ACCOUNT|6900
PU_CLERK|3100
PU_CLERK|2600
ST_MAN|5800
ST_CLERK|2100
ST_CLERK|3600
ST_CLERK|3100
SA_MAN|13500
SA_REP|7400
SA_REP|8600
SH_CLERK|3100
HR_REP|6500
AD_VP|17000
FI_MGR|12008
SA_REP|9000
SH_CLERK|2500
SH_CLERK|3000
SH_CLERK|3600
MK_REP|6000
AC_MGR|12008
IT_PROG|4800
FI_ACCOUNT|8200
PU_MAN|11000
PU_CLERK|2500
ST_CLERK|3300
SA_MAN|12000
SA_MAN|10500
SA_REP|7200
SH_CLERK|4200
SH_CLERK|4100
SH_CLERK|2900
AD_ASST|4400
IT_PROG|6000
PU_CLERK|2900
ST_MAN|8200
ST_CLERK|3200
ST_CLERK|2800
ST_CLERK|3500
ST_CLERK|2600
SA_REP|9500
SA_REP|10500
SA_REP|6400
SA_REP|11500
SA_REP|6100
SH_CLERK|2800
SH_CLERK|3400
SH_CLERK|2600
MK_MAN|13000
FI_ACCOUNT|7800
ST_CLERK|2700
ST_CLERK|2400
SA_MAN|14000
SA_MAN|11000
SA_REP|8000
SA_REP|9600
SH_CLERK|4000
IT_PROG|9000
IT_PROG|4200
ST_MAN|6500
ST_CLERK|2900
SA_REP|7000
SA_REP|6800
SA_REP|6200
SA_REP|11000
SA_REP|8400
SH_CLERK|3900
AD_PRES|24000
ST_MAN|8000
SA_REP|10000
SA_REP|7500
SA_REP|7300
SA_REP|8800
SH_CLERK|3200
SH_CLERK|3800
PR_REP|10000
FI_ACCOUNT|9000
FI_ACCOUNT|7700
PU_CLERK|2800
ST_MAN|7900
ST_CLERK|2200
ST_CLERK|2500
AC_ACCOUNT|8300

#### Zadanie 1.5

```
select street_address as "Ulica", postal_code as "Kod Pocztowy", 
    city as "Miasto", country_id as "Panstwo"
from locations;
```

Rezultat:

Ulica|Kod Pocztowy|Miasto|Panstwo
-- | -- | -- | --
1297 Via Cola di Rie|00989|Roma|IT
93091 Calle della Testa|10934|Venice|IT
2017 Shinjuku-ku|1689|Tokyo|JP
9450 Kamiya-cho|6823|Hiroshima|JP
2014 Jabberwocky Rd|26192|Southlake|US
2011 Interiors Blvd|99236|South San Francisco|US
2007 Zagora St|50090|South Brunswick|US
2004 Charade Rd|98199|Seattle|US
147 Spadina Ave|M5V 2L7|Toronto|CA
6092 Boxwood St|YSW 9T2|Whitehorse|CA
40-5-12 Laogianggen|190518|Beijing|CN
1298 Vileparle (E)|490231|Bombay|IN
12-98 Victoria Street|2901|Sydney|AU
198 Clementi North|540198|Singapore|SG
8204 Arthur St||London|UK
Magdalen Centre, The Oxford Science Park|OX9 9ZB|Oxford|UK
9702 Chester Road|09629850293|Stretford|UK
Schwanthalerstr. 7031|80925|Munich|DE
Rua Frei Caneca 1360 |01307-002|Sao Paulo|BR
20 Rue des Corps-Saints|1730|Geneva|CH
Murtenstrasse 921|3095|Bern|CH
Pieter Breughelstraat 837|3029SK|Utrecht|NL
Mariano Escobedo 9991|11932|Mexico City|MX

#### Zadanie 1.6

```
select region_name nazwa
from regions;
```

Rezultat:

| NAZWA |
| -- |
| Europe |
| Americas |
| Asia |
| Middle East and Africa |

#### Zadanie 1.7

```
select (4/2) * (4/2) * 3.14
from dual;
```

Rezultat:

| (4/2)*(4/2)*3.14 |
| -- |
| 12.56 |

#### Zadanie 1.8

```
select 2 * 8 - 4 as "wynik"
from dual;
```

Rezultat:

| wynik |
| -- |
| 12 |


#### Zadanie 1.9

```
select (3 * 3 + 5 * 5 * 5) / 2 as "wynik"
from dual;
```

Rezultat:

| wynik |
| -- |
| 67 |


#### Zadanie 1.10

```
select first_name, last_name, hire_date, 
    (40 * 365) + hire_date "Data Zakonczenia"
from employees;
```

Rezultat:

FIRST_NAME|LAST_NAME|HIRE_DATE|Data Zakonczenia
-- | -- | -- | --
Steven|King|17-JUN-03|07-JUN-43
Neena|Kochhar|21-SEP-05|11-SEP-45
Lex|De Haan|13-JAN-01|03-JAN-41
Alexander|Hunold|03-JAN-06|24-DEC-45
Bruce|Ernst|21-MAY-07|11-MAY-47
David|Austin|25-JUN-05|15-JUN-45
... | ... | ... | ...


#### Zadanie 1.11

```
select 'Krystian' || ' ' || 'Zieja' as "Nazwa"
from dual;
```

Rezultat:

| Nazwa |
| -- |
| Krystian Zieja |

#### Zadanie 1.12

```
select first_name || ' ' || last_name "Pracownik", salary "Pensja"
from employees;
```

Rezultat:

Pracownik|Pensja
-- | -- 
Steven King|24000
Neena Kochhar|17000
Lex De Haan|17000
Alexander Hunold|9000
Bruce Ernst|6000
David Austin|4800

#### Zadanie 1.13

```
select q'#Szanowny Pan'Pani #' || first_name || ' ' || last_name as "Naglowek"
from employees;
```

Rezultat:

| Naglowek |
| -- |
| Szanowny Pan'Pani Ellen Abel |
| Szanowny Pan'Pani Sundar Ande |
| Szanowny Pan'Pani Mozhe Atkinson |
| Szanowny Pan'Pani David Austin |
| Szanowny Pan'Pani Hermann Baer |
| Szanowny Pan'Pani Shelli Baida |
| Szanowny Pan'Pani Amit Banda |
| ... |

## Klauzula WHERE

#### Zadanie 2.1

```
select last_name, first_name, salary
from employees
where salary = 10000;
```

Rezultat:

LAST_NAME|FIRST_NAME|SALARY
-- | -- | --
Tucker|Peter|10000
King|Janette|10000
Bloom|Harrison|10000
Baer|Hermann|10000

#### Zadanie 2.2

```
select last_name, job_id
from employees
where job_id = 'Sa_Rep';
```

Rezultat:

no rows selected

#### Zadanie 2.3

```
select last_name, job_id
from employees
where job_id = 'SA_REP';
```

Rezultat:

LAST_NAME|JOB_ID
-- | --
Abel|SA_REP
Ande|SA_REP
Banda|SA_REP
Bates|SA_REP
Bernstein|SA_REP
Bloom|SA_REP
Cambrault|SA_REP
Doran|SA_REP
Fox|SA_REP
Grant|SA_REP
Greene|SA_REP
Hall|SA_REP
Hutton|SA_REP
Johnson|SA_REP
King|SA_REP
Kumar|SA_REP
... | ...


#### Zadanie 2.4

```
select first_name, last_name, salary
from employees
where first_name || ' ' || last_name = 'Steven King';
```

Rezultat:

FIRST_NAME|LAST_NAME|SALARY
-- | -- | --
Steven|King|24000


#### Zadanie 2.5

```
alter session set nls_date_format = 'DD-MON-RR';

```

Rezultat:

```
session SET altered.
```

#### Zadanie 2.6

```
select employee_id "numer pracownika"
from job_history
where start_date = '13-JAN-2001';
```

#### Zadanie 2.7

```
select employee_id 
from job_history
where start_date = end_date;
```

Rezultat:

No rows returned.

#### Zadanie 2.8

```
select employee_id, start_date+30
from job_history
where start_date + 30 = '12-FEB-01';
```

Rezultat:

EMPLOYEE_ID|START_DATE+30
--|--
102|12-FEB-01


#### Zadanie 2.9

```
select last_name, salary
from employees
where salary > 5000;
```

Rezultat:

LAST_NAME|SALARY
--|--
King|24000
Kochhar|17000
De Haan|17000
Hunold|9000

#### Zadanie 2.10

```
select last_name, salary
from employees
where salary < 4000;
```

LAST_NAME|SALARY
--|--
Khoo|3100
Baida|2900
Tobias|2800
Himuro|2600
Colmenares|2500


#### Zadanie 2.11

```
select last_name, commission_pct
from employees
where commission_pct >= 0.3
```

Rezultat:

LAST_NAME|COMMISSION_PCT
-- | --
Russell|0.4
Partners|0.3
Errazuriz|0.3
Cambrault|0.3
Tucker|0.3
King|0.35
Sully|0.35
McEwen|0.35
Smith|0.3
Doran|0.3
Abel|0.3

#### Zadanie 2.12

```
select last_name, commission_pct
from employees
where commission_pct <= 0.1;
```

Rezultat:

LAST_NAME|COMMISSION_PCT
--|--
Marvins|0.1
Lee|0.1
Ande|0.1
Banda|0.1
Kumar|0.1
Johnson|0.1


#### Zadanie 2.13

```
select first_name, last_name 
from employees
where salary != department_id * 100;
```

#### Zadanie 2.14

```
select employee_id, start_date
from job_history
where start_date > '01-FEB-2002';
```

Rezultat:

EMPLOYEE_ID|START_DATE
--|--
201|17-FEB-04
114|24-MAR-06
122|01-JAN-07
176|24-MAR-06
176|01-JAN-07
200|01-JUL-02


#### Zadanie 2.15

