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

Znajdź oraz wyświetl numer działu o nazwie IT.

```
declare 
  l_department_name varchar2(30) not null := 'IT';
  l_department_id number(6);
begin
  select department_id
    into l_department_id
    from departments
    where department_name = l_department_name;
    
  dbms_output.put_line('Numer dzialu ' || l_department_name || ' to ' || l_department_id);
end;
```

Korzystając z konstrukcji SELECT INTO  można pobrać w tym samym czasie więcej niż jedną wartość z tabeli.

#### Przykład 8.10

```
declare 
  l_last_name varchar2(30) not null := 'Gietz';
  l_employee_id number(6);
  l_salary number(6);
begin
  select employee_id, salary
    into l_employee_id, l_salary
    from employees
    where last_name = l_last_name;
    
  dbms_output.put_line(l_last_name || ' ma numer ' || l_employee_id || ' oraz zarabia ' || l_salary);
end;
```

## Stałe w PL/SQL

PL/SQL pozwala również na deklaracje stałych. Stała jest to zmienna, która nie może zmieniać wartości.

#### Przykład 8.11

Zadeklaruj stałą liczba pi o wartości 3.14 i oblicz pole koła o promieniu 5.

```
declare
  c_pi constant number(3,2) := 3.14;
  l_radius number(1) := 5;
begin
  dbms_output.put_line('Pole kola o promieniu ' || l_radius || ' wynosi ' || c_pi * l_radius * l_radius);
end;
```

#### Przykład 8.12

```
declare
  c_constant constant number(3,2);
begin
  dbms_output.put_line(c_constant);
end;
```

Rezultat:

```
ORA-06550: line 2, column 3:
PLS-00322: declaration of a constant 'C_CONSTANT' must contain an initialization assignment
ORA-06550: line 2, column 14:
```

#### Przykład 8.13

```
declare
  c_constant constant number(3,2) := 100;
begin
  c_constant := 200;
  dbms_output.put_line(c_constant);
end;
```

Rezultat:

```
ORA-06550: line 4, column 3:
PLS-00363: expression 'C_CONSTANT' cannot be used as an assignment target
ORA-06550: line 4, column 3:
```

## Typ rekordowy w Oracle

Typ rekordowy w Oracle przypomina obiekt lub wiersz z tabeli. Typ rekordowy posiada pola do przechowywania danych. Aby móc użyć typu rekordowego w Oracle najpierw musimy go zdefiniować.

Składnia definicji typu rekordowego:

```
TYPE record_type_name IS RECORD
(
    first_column datatype,
    second_column datatype,
    ...
);
```

#### Przykład 8.14

```
declare
  type region is record
  (
    region_id number,       
    region_name varchar2(25)
  );
  
  l_region region;
  l_region_id number not null := 1;
begin
  select region_id, region_name
    into l_region
  from regions
  where region_id = l_region_id;
  dbms_output.put_line('Region Id: ' || l_region.region_id);
  dbms_output.put_line('Region Name: ' || l_region.region_name);
end;
```

Należy pamiętać, że typ rekordowy nie musi odpowiadać liczbie kolumn w tabeli, a nawet może być całkowicie niezwiązany z żadną tabelą.


#### Przykład 8.15

```
declare
  type emp is record
  (
    first_name varchar2(30),       
    last_name varchar2(30),
    salary number,
    info varchar2(100)
  );
  
  l_emp emp;
  l_employee_id number not null := 100;
begin
  select first_name, last_name, salary
    into l_emp.first_name, l_emp.last_name, l_emp.salary
  from employees
  where employee_id = l_employee_id;
  
  l_emp.info := 'Zostanie zwolniony';
  dbms_output.put_line('Pracownik: ' || l_emp.first_name || ' ' 
    || l_emp.last_name || ' z pensja ' || l_emp.salary);
  dbms_output.put_line(l_emp.info);
end;
```

Jeżeli chcemy wykorzystać typ rekordowy do pobrania danych z tabeli, nie musimy definiować wszystkich kolumn możemy w definicji posłużyć się %ROWTYPE.

#### Przykład 8.16

```
declare
  l_region regions%rowtype;
  l_region_id number not null := 2;
begin
  select *
    into l_region
  from regions
  where region_id = l_region_id;
  
  dbms_output.put_line('Region Id: ' || l_region.region_id || ' ' 
    ||  ' Region Name: ' || l_region.region_name);
  
end;
```

## Wyrażenia warunkowe w PL/SQL

PL/SQL wspiera jak większość języków programowania intrukcje warunkową IF ELSEIF ELSE (UWAGA: w kodzie źródłowym ELSEIF zapisujemy jako ELSIF).

#### Przykład 8.17

```
declare
  l_salary number;
  l_employee_id number := 100;
begin
  select salary
    into l_salary
  from employees
  where employee_id = l_employee_id;
  
  if l_salary > 5000
  then
    dbms_output.put_line('Powyzej sredniej krajowej: ' || l_salary);
  end if;
end;
```

#### Przykład 8.18

```
declare
  l_salary number;
  l_employee_id number := 200;
begin
  select salary
    into l_salary
  from employees
  where employee_id = l_employee_id;
  
  if l_salary > 5000
  then
    dbms_output.put_line('Powyzej sredniej krajowej: ' || l_salary);
  else
    dbms_output.put_line('Ponizej sredniej krajowej: ' || l_salary);
  end if;
end;
```


#### Przykład 8.19

```
declare
  l_salary number;
  l_employee_id number := 200;
begin
  select salary
    into l_salary
  from employees
  where employee_id = l_employee_id;
  
  if l_salary < 3400
  then
    dbms_output.put_line('Ponizej sredniej krajowej: ' || l_salary);
  elsif l_salary > 3400
  then
    dbms_output.put_line('Powyzej sredniej krajowej: ' || l_salary);
  else
    dbms_output.put_line('Srednia krajowa: ' || l_salary);
  end if;
end;
```

## Pętle w PL/SQL

### Simple Loop

Najprostszą konstrukcją pętli w PL/SQLjest Simple Loop.

```
LOOP
    instrukcje do wykonania
    [EXIT]
    [EXIT WHEN warunek]
END LOOP;
```

Tą pętle wykorzystujemy gdy nie wiemy ile razy chcemy wykonać pętle, ale jesteśmy pewni, że chcemy aby ciało pętli zostało wykonane conajmniej raz. Jeżeli pętla nie będzie zawierała słowa kluczowego EXIT lub EXIT WHEN z warunkiem zakończenia pętli, będzie ona działać w nieskończonść.

#### Przykład 8.20

```
declare
  l_start_balance number := 2150;
  l_end_balance number := 1000;
begin
  
  loop
    l_start_balance := l_start_balance - 100;
    dbms_output.put_line('Biezacy balans: ' || l_start_balance);
    if l_start_balance < l_end_balance
    then
      exit;
    end if;
  end loop;
  
end;

```

#### Przykład 8.21

```
declare
  l_start_balance number := 2150;
  l_end_balance number := 1000;
begin
  
  loop
    l_start_balance := l_start_balance - 100;
    dbms_output.put_line('Biezacy balans: ' || l_start_balance);
    exit when l_start_balance < l_end_balance;
    
  end loop;
  
end;

```

### While Loop

Innym rodzajem pętli jest pętla WHILE. W tej pętli nie mamy gwarancji, że ciał zostanie wykonane conajmniej raz.

```
WHILE warunek
LOOP
    instrukcje
END LOOP;
```

#### Przykład 8.22

```
declare
  l_number number := 1;
  l_count number := 0;
begin
  
  while l_count < 10
  loop
    
    if mod(l_number, 2) != 0
    then
      dbms_output.put_line('liczba nieparzysta: ' || l_number);
      l_count := l_count + 1;
    end if;
    l_number := l_number + 1;
  end loop;
  
end;

```

### FOR Loop

```
FOR index IN [REVERSE] start .. koniec
LOOP
 instrukcje
END LOOP;

```

### Przykład 8.23

```
begin
  
  for i in 1..10
  loop
    dbms_output.put_line('index: ' || i);
  end loop;
  
end;
```

### Przykład 8.24

```
begin
  
  for i in reverse 1..10
  loop
    dbms_output.put_line('index: ' || i);
  end loop;
  
end;
```

Pętla FOR wspiera również interacje po rekordach zwróconych przez instrukcje SELECT.

### Przykład 8.25

```
begin
  
  for region_rec in (select * from regions)
  loop
    dbms_output.put_line('Region Id: ' || region_rec.region_id);
    dbms_output.put_line('Region Name: ' || region_rec.region_name);
    dbms_output.put_line('');
  end loop;
  
end;

```

### Przykład 8.26

```

```