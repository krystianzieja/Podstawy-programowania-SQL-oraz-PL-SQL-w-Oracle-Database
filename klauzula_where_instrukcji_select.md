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

