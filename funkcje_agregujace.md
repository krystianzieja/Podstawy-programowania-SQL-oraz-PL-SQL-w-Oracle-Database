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

**UWAGA: Funkcje AVG, SUM, VARIANCE oraz STDDEV mogą być wykorzystane tylko z typami danych numerycznymi.**

Funkcje MIN oraz MAX można wykorzystać również z danymi znakowymi.

#### Przykład 5.5

Wybierz "najmniejsze" oraz "największe" nazwisko z tabeli EMPLOYEES.

```
select min(last_name), max(last_name)
from employees;
```

#### Zadanie 5.1

Wyświetl największą oraz najmniejszą prowizję (kolumna: COMMISSION_PCT) z tabeli EMPLOYEES.

#### Przykład 5.6

Wyświetl liczbę pracowników z tabeli EMPLOYEES.

```
select count(*)
from employees;
```

#### Przykład 5.7

Wyświetl liczbę pracowników z tabeli EMPLOYEES, którzy mają zdefiniowaną prowizję. 

```
select count(commission_pct)
from employees;
```

#### Zadanie 5.2

Wyświetl liczbę pracwoników z działu (kolumna: DEPARTMENT_ID) 80 z tabeli EMPLOYEES.

#### Zadanie 5.3

Wyświetl liczbę działów, w kótych pracują pracownicy, korzystając z tabeli EMPLOYEES.


## Funkcje agregujące, a wartości NULL

Funkcje agregujące pomijają wartości NULL. Jeżeli chcemy, żeby funkcja agregująca brałą pod uwagę wartości NULL, muszą one zostać zamienione na wartości nie bedące NULL'ami np. poprzez wykorzystanie funkcji NVL.

#### Przykład 5.8

Wyświetl średnia prowizję (kolumna: COMMISSION_PCT) dla pracowników z pominięciem wartości NULL, oraz uwzględniając wartości NULL.

```
select avg(commission_pct), avg(nvl(commission_pct, 0))
from employees;
```

Składnia dla zapytania z funkcją agregującą, które tworzy grupy

```
select kolumna, funkcja_agregujące(kolumna)
from tabela
[ where warunek ]
[ group by wyrazenie_group_by ]
[ order by kolumna ]
```

Za zdefiniowanie grup rekordów, na których działać będzie funkcja agregująca, odpowiedzialna jest klauzula GROUP BY.

**wyrazenie_group_by** definiuje kolumny, których wartości posłużą do zdefiniowania grup.

Jeżeli użyliśmy funkcji agregującej na liście SELECT, nie możemy tam umieścić kolumn, które nie występują w klauzuli GROUP BY.

#### Przykład 5.9

Wybierz nazwisko/a pracownika/ów, który/zy zarabia najmniej (kolumna: SALARY).

```
select last_name, min(salary)
from employees;
```

Rezultat:

```
ORA-00937: not a single-group group function
00937. 00000 -  "not a single-group group function"
*Cause:    
*Action:
Error at Line: 40 Column: 8
```

Prawidłowe rozwiązaniej to posłużenie się podzapytaniem.

```
select last_name, salary
from employees 
where salary = (
  select min(salary)
  from employees);
```

Korzystając z klauzuli where możemy wyeliminować rekordy, zanim zostaną utworzone grupy poprzez klauzulę GROUP BY.

Nie można wykorzystać aliasów kolumn, w klauzuli GROUP BY.

#### Przykład 5.10

Wyświetl maksymalną oraz minimalną pensję (kolumna: SALARY), w każdym dziale za wyjątkiem działu numer 80 (kolumna: DEPARTMENT_ID). Posortuj rezultat po numerze działu.

```
select department_id, min(salary), max(salary)
from employees
where department_id <> 80
group by department_id
order by department_id;
```

#### Zadanie 5.4

Wyświetl średnia płacę w każdym z działów, wynik posortuj po numerze działu.

**UWAGA:** Należy zwrócić uwagę, że rezultat zawiera grupę utworzoną dla pracowników, którzy nie są przypisani do żadnego działu.


Należy pamiętać, że kolumna, którą wykorzystujemy w klazuli GROUP BY nie musi występować na liście SELECT.

#### Przykład 5.11

Wyświetl data pierwszego zatrudnienia w każdym z działów, skorzystaj z tabeli EMPLOYEES. Nie umieszczaj kolumny DEPARTMENT_ID na liście SELECT.

```
select min(hire_date)
from employees
group by department_id;
```

W klauzuli GROUP BY możemy oczywiście wykorzystać więcej niż jedną kolumnę.

#### Przykład 5.12

Wyświetl maksymalną pensję (kolumna: SALARY) dla każdego stanowiska (kolumna JOB_ID) w każdym z działów (kolumna DEPARTMENT_ID). Wynik posortuj po numerze działu malejąco oraz stanowisku rosnąco.

```
select department_id, job_id, max(salary)
from employees
group by department_id, job_id
order by department_id desc, job_id asc;
```

#### Zadanie 5.5

Wyświetl ile firma przeznacza na wypłatę wynagrodzenia dla każdego stanowiska.

```

```
