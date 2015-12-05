# Klauzula WHERE instrukcji SELECT

Klauzula WHERE pozwala na zwrócenie tylko rekordów spełniających określone warunki, czyli wykonanie operacji selekcji.

* SELECT ... FROM ... Zwraca wszystkie rekordy z tabeli
* SELECT DISTINCT ... FROM ... Eliminuje duplikaty
* SELECT ... FROM ... WHERE ... pozwala na odczytanie rekordów spelniających określone warunki

Klauzula WHERE musi zawierać conajmniej jeden warunek.

#### Przykład 2.1

Wyświetl nazwę państwa (kolumna: CONTRY_NAME) dla państwa o kodzie MX (kolumna: COUNTRY_ID) z tabeli COUNTRIES.

```
select country_name
from countries
where country_id = 'MX';
```

Rezultat:

| COUNTRY_NAME |
| -- |
| Mexico |

#### Przykład 2.2

Wyświetl nazwy państ (kolumna: COUNTRY_NAME) znajdujące się w regionie (kolumna: REGION_ID) o identyfikatorze 3 z tabeli COUNTRIES. W raporcie umieść równieć kolumnę z identyfikatorem regionu.

```
select country_name, region_id
from countries
where region_id = 3;
```

Rezultat:

COUNTRY_NAME|REGION_ID
-- | --
Australia|3
China|3
India|3
Japan|3
Malaysia|3
Singapore|3

#### Zadanie 2.1

Wyświetl nazwisko (kolumna: LAST_NAME), imię (kolumna: FIRST_NAME) oraz pensję (kolumna: SALARY) pracowników zarabiających 10000.

### Stringi oraz Daty w klauzuli WHERE

* Ciągi znakowe oraz Daty muszą być otoczone pojedyńczym cudzysłowiem. 
* Oracle przechowuje ciągi znaków z zachowaniem wielkości znaków ("case-sensitive") 
* Oracle ma wiele formatów daty, więc najbezpieczniej jest zawsze skorzystać z funkcji TO_DATE
 
W warunkach klauzuli WHERE oprócz stałych można wykorzystać kolumny. 

#### Przykład 2.3

Wyświetl pracowników, których pensja jest 90-cio krotnością numeru działu, w którym pracują.

```
select last_name, salary, department_id
from employees
where salary = 90 * department_id;
```

Rezultat:

LAST_NAME|SALARY|DEPARTMENT_ID
-- | -- | --
Faviet|9000|100
Marvins|7200|80

#### Zadanie 2.2

Wyświelt nazwiska (kolumna: LAST_NAME) wszystkich pracowników, którzy pracują na stanowisku 'Sa_Rep'.

#### Zadanie 2.3

Wyświelt nazwiska (kolumna: LAST_NAME) wszystkich pracowników, którzy pracują na stanowisku 'SA_REP'.

### Konkatenacja klauzulu WHERE

Operacje konkatenacji można wykorzystać nie tylko liście select, ale również w klauzuli WHERE.

#### Przykład 2.4

Wyświetl nazwisko (kolumna: LAST_NAME) oraz imię (kolumna: FIRST_NAME), dla pracowników dla których konkatenacja kolumn JOB_ID oraz LAST_NAME wynosi SA_REPKing.

```
select last_name, first_name
from employees
where job_id || last_name = 'SA_REPKing';
```

#### Zadanie 2.4

Wyświetl imię (kolumna: FIRST_NAME), nazwisko (kolumna: LAST_NAME), oraz pensję (kolumna: SALARY) dla pracowników z tabeli EMPLOYEES dla, których konkatenacja imienia oraz nazwiska to 'Steven King'. 

### Daty w bazie danych Oracle

Wykorzystując w Oracle kolumny z typem danych DATE, należy pamiętać o kilku rzeczach:

* Ciąg znakowy reprezentujący datę należy otoczyć pojedyńczymi znakami cudzysłowia, np. '11-Dec-15'
* Data w Oracle jest przechowywana jako liczba
* Oracle wykona automatyczną konwersje ciągu znakowego na typ danych typu DATE, korzystając z domyślnego formatu DD-MON-RR
* RR jest odpowiedzialny za rok. Jeżeli RR > 50 doczepiamy poprzednie stulecie np. 99 daje 1999. W przeciwnym razie bieżace 19 daje 2019.

Domyślny format danych może zostać zmieniony dla całej instancji, albo dla sesji.
Format ustawiony na instancji będzie działał dla wszystkich sesji, ustawienie dla sesji będzie działać tylko dla bieżącej sesji do momentu jej rozłączenia lub ponownej zmiany formatu daty dla sesji.

#### Przykład 2.5

Aby sprawdzić bierzące ustawienie formatu daty dla sesji należy skorzystać z NLS_SESSION_PARAMETERS.

```
select parameter, value
from nls_session_parameters
where parameter = 'NLS_DATE_FORMAT'
```

Rezultat:

PARAMETER|VALUE
--|--
NLS_DATE_FORMAT|DD-MON-RR

W celu zmiany formatu dla sessji należy wykorzystać instrukcję ALTER SESSION. Zmiana ustawień na poziomie instancji wymaga uprawnień administratora.

#### Przykład 2.6

Wyświetl nazwisko (kolumna: LAST_NAME) oraz datę zatrudnienia (kolumna: HIRE_DATE) dla pracowników zatrudnionych 21-go września 2005 roku - wykorzystaj format daty '21-10-2005'

```
select last_name, hire_date
from employees
where hire_date = '21-09-2005'
```

Rezultat:

```
ORA-01843: not a valid month
01843. 00000 -  "not a valid month"
*Cause:    
*Action:
```

Alternatywną opcją wykorzystania innego formatu daty jest wykorzystanie funkcji TO_DATE.


#### Przykład 2.7

Zmień format daty dla sesji na dd-mm-yyyy i wykonaj ponownie zadanie z przykładu 2.6

```
alter session set nls_date_format = 'dd-mm-yyyy';
```

Rezultat:

```
session SET altered.
```

```
select last_name, hire_date
from employees
where hire_date = '21-09-2005';
```

Rezultat:

LAST_NAME|HIRE_DATE
--|--
Kochhar|21-09-2005


#### Zadanie 2.5

Zmień format daty dla sessji na DD-MON-RR.


#### Zadanie 2.6

Wybierz numery pracowników (kolumna: EMPLOYEE_ID), nadaj tej kolumnie alias numer pracownika, z tabeli JOB_HISTORY, którzy zaczeli pracować (kolumna: START_DATE) 13 stycznia 2001 roku.

#### Zadanie 2.7

Wybierz numery pracowników (kolumna: EMPLOYEE_ID), którzy zaczeli i zakończyli pracę tego samego dnia (kolumny: START_DATE, END_DATE) z tabeli JOB_HISTORY.

#### Zadanie 2.8

Wybierz numery pracowników (kolumna: EMPLOYEE_ID), którzy zaczeli pracować 30 dni przed 12-tego lutego 2001 roku.


## Operatory w klauzuli WHERE

Oprócz operatora równości w klauzuli WHERE możemy zastosować inne operatory.

Operator | Znaczenie
-- | --
< | Mniejsze
> | Większe
<= | Mniejsze równe
>= | Większe równe
<> | Różne
!= | Różne

#### Zadanie 2.9

Wybierz nazwiska (kolumna: LAST_NAME) oraz pensje (kolumna: SALARY) z tabeli EMPLOYEES, pracowników zarabiających więcej niż 5000.

#### Zadanie 2.10

Wybierz nazwiska (kolumna: LAST_NAME) oraz pensje (kolumna: SALARY) z tabeli EMPLOYEES, pracowników zarabiających mniej niż 4000.


#### Zadanie 2.11

Wybierz nazwiska (kolumna: LAST_NAME) oraz prowizję (kolumna: COMMISSION_PCT) z tabeli EMPLOYEES, pracowników mających prowizję większą lub równą 0.3


#### Zadanie 2.12

Wybierz nazwiska (kolumna: LAST_NAME) oraz prowizję (kolumna: COMMISSION_PCT) z tabeli EMPLOYEES, pracowników mających prowizję mniejszą lub równą 0.1


#### Zadanie 2.13

Wybierz imiona (kolumna: FIRST_NAME) oraz nazwiska (kolumna: LAST_NAME) z tabeli EMPLOYEES pracowników dla, których wartość ich pensji (kolumna: SALARY) nie jest równa ich stukrotności numeru działu (kolumna: DEPARTMENT_ID), w którym pracują.

#### Zadanie 2.14

Wybierz numery pracowników (kolumna: EMPLOYEE_ID) oraz datę początku pracy (kolumna: START_DATE). którzy zaczeli pracować po 1-szym lutego 2002 roku. Tabela JOB_HISTORY.

#### Zadanie 2.15

Wyświetl listę działów, których nazwa (kolumna: DEPARTMENT_NAME) jest inna niż IT z tabeli DEPARTMENTS.

Operatory <, >, <=, >= mogą zostać również do ciągów znakowych.

#### Przykład 2.8

Wybierz nazwiska pracowników z tabeli, które są mniejsze niż Bell.

```
select last_name 
from employees
where last_name < 'Bell';
```

Rezultat:

| LAST_NAME |
| -- |
| Abel |
| Ande |
| Atkinson |
| Austin |
| Baer |
| Baida |
| Banda |
| Bates |


W takiej sytuacji ciąg znakowy jest konwertowany do wartości numerycznej znak po znaku. Uwaga!!! Wielkość znaków ma znaczenie, czyli 'b' != 'B'.


#### Przykład 2.9

Wybierz nazwiska pracowników z tabeli, które są mniejsze niż bell.

```
select last_name 
from employees
where last_name < 'bell';
```

Rezultat:

| LAST_NAME |
| -- |
| Abel |
| Ande |
| ... |
| Whalen |
| Zlotkey |

Jak widać wszystkie rekordy zostały zwrócone, dlatego, że wszystkie wielkie litery alfabetu mają mniejszą wartość numeryczną niż małe litery.

## Operator BETWEEN AND

Operator BETWEEN jest operatorem zakresowym, czyli pozwala wybrać rekordy spełniajace warunke "od" "do".

#### Przykład 2.10

Wybierz nazwisko (kolumna: LAST_NAME) oraz pensję (kolumna: SALARY) pracowników zarabiających pomiędzy 3000, a 4000 z tabeli EMPLOYEES. Wykorzystaj operator BETWEEN AND.

```
select last_name, salary
from employees
where salary between 3000 and 4000;
```

Rezultat:

LAST_NAME|SALARY
-- | --
Khoo|3100
Nayer|3200
Bissot|3300
Mallin|3300
Ladwig|3600
Stiles|3200
Rajs|3500
Davies|3100
Taylor|3200
Fleaur|3100
Dellinger|3400
Cabrio|3000
Chung|3800
Dilly|3600
Bell|4000
Everett|3900
McCain|3200
Walsh|3100
Feeney|3000

UWAGA!!! W operatorze BETWEEN podane zakresy wchodzą jako spełniające warunek, czyli BETWEEN AND przekłada się na >=, <=.

Operator BETWEEN może zostać również wykorzystany przy pracy z datami.

#### Przykład 2.11

Wyberz numer pracownika (kolumna EMPLOYEE_ID), oraz datę początku pracy (kolumna: START_DATE) z tabeli JOB_HISTORY, którzy zaczeli pracę pomiędzy 1-szym czerwca 2001, a 1-szym czerwca 2003.

```
select employee_id, start_date
from job_history
where start_date between '01-JUN-01' and '01-JUN-03';
```

EMPLOYEE_ID|START_DATE
--|--
101|28-OCT-01
200|01-JUL-02

#### Zadanie 2.16

Wyświetl numery (kolumna: DEPARTMENT_ID) oraz nazwy działów (kolumna: DEPARTMENT_NAME) z tabeli DEPARTMENTS, działów mających numery pomiędzy 30, a 50.

## Operator IN

Operator IN sprawdza czy wartość znajduje się w podanym zbiorze.

#### Przykład 2.12

Wybierz pracowników zarabiających 1000, 2000, 4000 z tabeli EMPLOYEES.

```
select first_name, last_name, salary
from employees
where salary in (1000, 2000, 4000);
```

Rezultat:

FIRST_NAME|LAST_NAME|SALARY
-- | -- | --
Sarah|Bell|4000

#### Przykład 2.13

Wyświetl imiona, nazwiska oraz pensję pracowników z nazwiskami King, Bell oraz Adel z tabeli EMPLOYEES.

```
select first_name, last_name, salary
from employees
where last_name in ('King', 'Bell', 'Abel');
```

Rezultat:

FIRST_NAME|LAST_NAME|SALARY
--|--|--
Ellen|Abel|11000
Sarah|Bell|4000
Janette|King|10000
Steven|King|24000

#### Przykład 2.14

Wyświetl nazwiska pracowników i datę ich zatrudnienia (kolumna: HIRE_DATE) zatrudnionych 7-ego czerwca 2002 roku oraz 1-ego grudnia 1999.

```
select last_name, hire_date
from employees
where hire_date in ('07-JUN-02','01-DEC-99');
```

Rezultat:

LAST_NAME|HIRE_DATE
--|--
Mavris|07-JUN-02
Baer|07-JUN-02
Higgins|07-JUN-02
Gietz|07-JUN-02


#### Zadanie 2.17

Wyświetl nazwy działów (kolumna: DEPARTMENT_NAME) oraz  numery działów, dla numerów działów (kolumna: DEPARTMENT_ID) 10,20,30.

#### Zadanie 2.18

Wybierz ulicę (kolumna: STREET_ADDRESS), kod pocztowy (kolumna: POSTAL_CODE) oraz miasto (kolumna: CITY) z tabeli LOCATIONS dla miejsc w USA i Wielkiej Brytanii. Wykorzystaj kolumnę COUNTRY_ID i odpowiednie kody państw.


## Operator LIKE

Operator LIKE pozwala przeszukiwać wartości w celu znalezienia wzorca. Pozwala on na wykorzystanie znaków WILDCARD, które zastępują inne znaki zgodnie z poniższymi zasadami.

* % - zastępuje 0 lub więcej znaków
* _ - zastępuje jeden znak
 

#### Przykład 2.19

Wyświetl imiona i nazwiska pracowników z tabeli EMPLOYEES, których imiona zaczynają się na A.

```
select first_name, last_name
from employees
where first_name like 'A%';
```

Rezultat:

FIRST_NAME|LAST_NAME
--|--
Amit|Banda
Alexis|Bull
Anthony|Cabrio
Alberto|Errazuriz
Adam|Fripp
Alexander|Hunold
Alyssa|Hutton
Alexander|Khoo
Allan|McEwen
Alana|Walsh

#### Przykład 2.20

Wyświetl imiona i nazwiska pracowników z tabeli EMPLOYEES, którzy mają nazwisko King korzystając z operatora LIKE.

```
select first_name, last_name
from employees
where last_name like 'King';
```

Rezultat:

FIRST_NAME|LAST_NAME
--|--
Janette|King
Steven|King


#### Przykład 2.21

Wyświetl imiona i nazwiska pracowników z tabeli EMPLOYEES, którzy mają czteroliterowe nazwisko zaczynające się na K a kończące na ing korzystając z operatora LIKE.

```
select first_name, last_name
from employees
where last_name like 'K_ng';
```

FIRST_NAME|LAST_NAME
--|--
Janette|King
Steven|King
