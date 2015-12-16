# Funkcje Agregujące

Funkcje agregujące działają na zbiorach wierszy, ay zwrócić jeden rezultat dla grupy.

Podstawowa składnia zapytania z funkcją agregującą

```
select funkcja_agregujące(kolumna)
from tabela
[ where warunek ]
[ group by wyrazenie_group_by ]
[ order by kolumna ]
```

Podstawowe funkcje agregujące

Funkcja | Opis
-- | --
AVG( [DISTINCT lub ALL] n) | Średnia wartość n, ignorując wartości NULL
COUNT({ [DISTINCT lub ALL] expr}) | Liczba wierszy, dla których wyrażenie expr zwraca wartość inną niż NULL. W celu policzenia wszystkich wierszy można wykorzystać znak *
MAX( [DISTINCT lub ALL] expr) | Maksymalna  wartość expr, ignorując wartości NULL
MIN( [DISTINCT lub ALL] expr) | Minimalna  wartość expr, ignorując wartości NULL
STDEV( [DISTINCT lub ALL] expr) | Standardowe odchylenie dla expr, ignorując wartości NULL
SUM( [DISTINCT lub ALL] expr) | Suma wartości expr, ignorując wartości NULL
VARIANCE( [DISTINCT lub ALL] expr) | Wariancja expr, ignorując wartości NULL


