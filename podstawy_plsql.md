# Podstawy PL/SQL

## Pierwszy program w PL/SQL

#### Przykład 8.1

Napisz program (blok anonimowy) w PL/SQL, który wypisze na ekran "Hello World!".

```
begin
  dbms_output.put_line('Hello World!');
end;
```

Jak można łatwo zauważyć, że nic nie zostało wypisane na ekran. Powodem takiego zachowania jest domyślna konfiguracja narzędzi Oracle'a, które wypisywanie na ekran mają domyślnie wyłączone.

#### Przykład 8.2

Włącz wypisywanie na konsolę poprzez instrukcję SET SERVEROUTPUT ON i wykonaj popnownie blok anonimowy z Przykładu 8.1

```
set serveroutput on
begin
  dbms_output.put_line('Hello World!');
end;
```

Oracle pozwala na skorzystanie z komendy EXECUTE (w skrócie EXEC) w celu wykonania pojedyńczej funkcji lub procedury PL/SQL, co pozwala nam zaoszczędzić czas na pisanie BEGIN oraz END.

#### Przykład 8.3

Wypisz na ekran Hello World! korzystając z komendy EXECUTE.

```
exec dbms_output.put_line('Hello World!');
```

## Deklarowanie zmiennych

Zmienne w programach PL/SQL deklarujemy w bloku DECLARE dla bloków anonimowych lub bezpośrednio za sekcją nagłówkową w przypadku procedur oraz funkcji. (UWAGA: Są wyjątki od tej zasady).

Składnia do zadeklarowania zmiennej:

```
variable_name datatype [NOT NULL := value ]; 
```

#### Przykład 8.4

```
declare 
  l_name varchar2(20);
begin
  l_name := 'Krystian';
  dbms_output.put_line(l_name);
end;
```


#### Przykład 8.5

```
declare 
  l_emp_id number(6) := 1194;
  l_salary number(6) := 4500;
begin
  dbms_output.put_line('Pracownik ' || l_emp_id || ' zarabia ' || l_salary || ' PLN');
end;
```

#### Przykład 8.6

Zadeklaruj zmienną jako NOT NULL, ale nie przypisuj jej wartości.

```
declare 
  l_emp_id number(6) not null;
  l_salary number(6) := 4500;
begin
  dbms_output.put_line('Pracownik ' || l_emp_id || ' zarabia ' || l_salary || ' PLN');
end;
```

Rezultat:

```
Error report -
ORA-06550: line 2, column 12:
PLS-00218: a variable declared NOT NULL must have an initialization assignment
06550. 00000 -  "line %s, column %s:\n%s"
*Cause:    Usually a PL/SQL compilation error.
*Action:
```

#### Przykład 8.7

Popraw przykład 8.6 korzystajać ze słowa kluczowego DEFAULT.

```
declare 
  l_emp_id number(6) not null default 2244;
  l_salary number(6) := 4500;
begin
  dbms_output.put_line('Pracownik ' || l_emp_id || ' zarabia ' || l_salary || ' PLN');
end;
```

W celu pobrania pojedyńczej wartości z bazy danych i przypisanie jej do zmiennej możemy posłużyć się instrukcją SELECT INTO.

#### Przykład 8.8

```
declare 
  l_emp_id number(6) not null := 170;
  l_salary number(6);
begin
  select salary
    into l_salary
    from employees
    where employee_id = l_emp_id;
    
  dbms_output.put_line('Pracownik ' || l_emp_id || ' zarabia ' || l_salary || ' PLN');
end;
```

#### Przykład 8.9

```

```