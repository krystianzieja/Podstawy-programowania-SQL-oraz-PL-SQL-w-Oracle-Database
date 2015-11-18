# Instrukcja SELECT

## Podstawy instrukcji SELECT

Instrukcja SELECT pozwala na wybranie rekordów z tabeli lub perspektywy.

SELECT zapewnia funkcje takie jak:

* Projekcja (kolumny)
* Selekcja (wiersze)
* Złączenia (możliwość połączenia więcej niż jednej tabeli)


Podstawowa składnia instrukcji SELECT.

```
SELECT koluna1, kolumna2, ...
FROM tabela
```

Jednym z podstawowych rozszerzeń instrukcji SELECT jest wykorzystanie "*" zamiast listy kolumn, które chcemy wybrać. Wykorzystanie "*" oznacza, że wybieramy wszystkie kolumny z tabeli.

```
SELECT *
FROM tabela

```


Przykład 1.1:

Wyświetl całą zawartość tabeli z regionami geograficznymi (nazwa tabeli: REGIONS).

```
select *
from regions;
```

Rezultat:


| REGION_ID | REGION_NAME |
| -- | -- |
| 1 | Europe |
| 2 |Americas |
| 3 |Asia |
| 4 | Middle East and Africa |


Instrukcja SELECT pozwala nam rownież wyspecyfikować kolumny, którymi jesteśmy zainteresowani, służy do tego "lista select", czyli lista nazw kolumn, którą podajemy po słowie kluczowym SELECT.

Przykład 1.2:

Alternatywnym rozwiązaniem zadania z Przykładu 1.1 jest specyfikacja wszystkich kolumn z tabeli REGIONS.

```
select region_id, region_name
from regions;
```

Rezultat:


| REGION_ID | REGION_NAME |
| -- | -- |
| 1 | Europe |
| 2 |Americas |
| 3 |Asia |
| 4 | Middle East and Africa |

Oczywiście często nie będziemy zinteresowani wszystkimi kolumnami w danej tabeli, wtedy wystarczy wyspecyfikować kolumny, które chcemy pobrać z bazy danych na liście select.

Przykład 1.3:

Wybierz nazwy regionów geograficznych (nazwa tabeli: REGIONS, nazwa kolumny REGION_NAME).

```
select region_name
from regions;
```

Rezultat:

| REGION_NAME |
| -- |
| Europe |
| Americas |
| Asia |
| Middle East and Africa |


Zadanie 1.1:

Wybierz identyfikator pracownika (kolumna:  EMPLOYEE_ID), identyfikator stanowiska (kolumna: JOB_ID), identyfikator departamentu (kolumna: DEPARTMENT_ID) z tabeli JOB_HISTORY.

Zadanie 1.2:

Wyświetl całą zawartość tabeli ze stanowiskami (tabela: JOBS)


## DISTINCT

Słowo kluczowe DISTINCT pozwala usunąć duplikaty z rezultatu zwracanego przez instrukcję SELECT.

**UWAGA:** Wykorzystanie DISTINCT na dużej tabeli może mieć negatywny wpływ na wydajność.

Przykład 1.4:

Wybierz listę wszystkich stanowisk (kolumna: JOB_ID) z tabeli JOB_HISTORY eliminując duplikaty.

```
select distinct job_id
from job_history;
```

Rezultat:

| JOB_ID |
| -- |
| AC_ACCOUNT |
| AC_MGR |
| AD_ASST |
| IT_PROG |
| MK_REP |
| SA_MAN |
| SA_REP |
| ST_CLERK |


