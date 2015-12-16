# Funkcje Agregujące

Funkcje agregujące działają na zbiorach wierszy, ay zwrócić jeden rezultat dla grupy.

Podstawowa składnia zapytania z funkcją agregującą

```
select funkcja_agregujące(kolumna)
from tabela
[ where warunek ]
[ order by kolumna ]
```

Podstawowe funkcje agregujące

Funkcja | Opis
-- | --
AVG( [DISTINCT lub ALL] n) | Średnia wartość n, ignorując wartości NULL
