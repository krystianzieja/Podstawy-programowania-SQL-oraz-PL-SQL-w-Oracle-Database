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


Przykład 1.2:

Alternatywnym rozwiązaniem zadania z Przykładu 1.1 jest specyfikacja wszystkich kolumn z tabeli REGIONS.

