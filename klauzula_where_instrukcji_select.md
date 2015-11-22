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

