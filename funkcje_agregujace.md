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
STDDEV( [DISTINCT lub ALL] expr) | Standardowe odchylenie dla expr, ignorując wartości NULL
SUM( [DISTINCT lub ALL] expr) | Suma wartości expr, ignorując wartości NULL
VARIANCE( [DISTINCT lub ALL] expr) | Wariancja expr, ignorując wartości NULL

Słowo kluczowe DISTINCT powoduje, że funkcja agregująca pomija duplikaty. 
Słowo kluczowe ALL powoduje, że funkcja agregująca bierze pod uwagę wszystkie wartości. Słowo kluczowe ALL jest domyślne dla każdej funkcji agregującej, dlatego zwyczajowo się go nie pisze w kwerendach.

#### Przykład 5.1

Oblicz średnią płacę w firmie.

```
select avg(salary)
from employees;

```

#### Przykład 5.2

Wyświetl najmniejszą oraz największą pensję dla pracowników, których nazwa stanowska zawiera REP.

```
select min(salary), max(salary)
from employees
where job_id like '%REP%';
```

#### Przykład 5.3

Wyświetl sumę pensji z tabeli EMPLOYEES. Porównaj działanie słów kluczowych DISTINCT oraz ALL.

```
select sum(salary), sum(all salary), sum(distinct salary)
from employees;
```

Funkcję agregujące można również wykorzystać do pracy z typami danych typu DATE.

#### Przykład 5.4 

Wyświetl datę pierwszego zatrudnienia i ostatniego zatrudnienia.

```
select min(hire_date), max(hire_date)
from employees;
```

**UWAGA: Funkcje AVG, SUM, VARIANCE oraz STDDEV