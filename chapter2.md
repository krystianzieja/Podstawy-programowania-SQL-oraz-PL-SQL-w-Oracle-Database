# Instrukcja SELECT

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

