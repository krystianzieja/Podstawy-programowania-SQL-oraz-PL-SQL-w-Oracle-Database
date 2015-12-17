# Operatory zbiorowe

W Oracle występują cztery operatory zbiorowe. Wykorzystujemy je do pracy ze "złożonymi kwerendami", czyli kwerendami, które zawierają więcej niż jedną instrukcję SELECT.

Operator | Znaczenie
-- | -- 
UNION | Zwraca wiersze z obydwu kwerend, eliminujać duplikaty
UNION ALL | Zwraca wiersze z obydwu kwerend , nie eliminując duplikatów
INTERSECT | Zwraca wiersze, które występują w obydwu kwerendach
MINUS | Zwraca wiersze z pierwszej kwerendy, któe nie występują w drugiej kwerendzie

Wszystkie powyższe operatory mają taką samą ważność, co powoduje, że Oracle je rozpatruje od góry do dołu zgodnie z miejscem występowania w kwerendzie.

Liczba wyrażeń na listach SELECT musi być taka sama.

Typ danych kolumn w drugiej kwerendzie musi odpowiadać pierwszej kwerendzie.

Możmy wykorzystać nawiasy, aby zmienić koleność wykonania kwerend.

Klauzula ORDER BY może być użyta tylko na samym końcu całej instrukcji.

#### Przykład 6.1

Wyświetl wszystkie stanowiska (kolumna: JOB_ID), na których pracował dany pracownik (kolumna: EMPLOYEE_ID) oraz działy, w których pracował pracownik (kolumna: DEPARTMENT_ID). Skorzystaj z tabel: EMPLOYEES oraz JOB_HISTORY. Posortuj rezultat po kolumnie EMPLOYEE_ID.

```
select employee_id, job_id, department_id
from employees
union
select employee_id, job_id, department_id
from job_history
order by employee_id;
```

Zwróc uwagę na pracowników z identyfikatorami: 101 oraz 200.

#### Przykład 6.2

Wykonaj Przykład 6.1 korzystając z operatora UNION ALL. Porównaj rezultat z Przykładów 6.1 oraz 6.2 dla pracownika o EMPLOYEE_ID = 176.

```
select employee_id, job_id, department_id
from employees
union all
select employee_id, job_id, department_id
from job_history
order by employee_id;
```

#### Przykład 6.3 

Wykonaj kwerendę z przykładu 6.1 usuwając klauzulę ORDER BY.

```
select employee_id, job_id, department_id
from employees
union
select employee_id, job_id, department_id
from job_history;
```

Jak można łatwo zauważyć Oracle automatycznie wykonał sortowanie po pierwszej kolumnie na liście SELECT.


#### Przykład 6.4

Wyświetl pracowników, którzy mają teraz takie same stanowisko (kolumna: JOB_ID z tabeli EMPLOYEES), jakie mieli w przeszłości (kolumna: JOB_ID z tabeli JOB_HISTORY).

```
select employee_id, job_id
from employees
intersect
select employee_id, job_id
from job_history;
```

#### Zadanie 6.1

Wyświetl pracowników, którzy mają teraz takie same stanowisko (kolumna: JOB_ID z tabeli EMPLOYEES), jakie mieli w przeszłości (kolumna: JOB_ID z tabeli JOB_HISTORY). Dodatkowym wymaganiem jest, żeby pracownik pracował cały czas w tym samym dziale.


#### Przykład 6.5

Wyświetl pracowników z tabeli EMPLOYEES, którzy nigdy nie zajmowali innego stanowisko(czyli takich, którzy nie mają żadnego rekordu w tabeli JOB_HISTORY).

```
select employee_id
from employees
minus
select employee_id
from job_history;
```

Należy pamiętać, że listy SELECT w kwerendzie złożonej muszą zawierać taką samą liczbę wyrażeń oraz, że te wyrażenia muszą posiadać ten sam typ danych. Jeżeli nie jest to możliwe jedną z list SELECT, musimy doopełnić wyrażeniem zakodowanym na sztywno.

#### Przykład 6.6

Wyświetl wszystkie pensję (kolumna: SALARY) dla pracowników (kolumna: EMPLOYEE_ID) i danego stanowiska (kolumna: JOB_ID), które są wypłacane teraz tabela EMPLOYEES lub były wypłacane w przeszłości (tej informacji nie ma więc posłuż się wartością 0).

```
select employee_id, job_id, salary
from employees
union all
select employee_id, job_id, 0
from job_history;
```
