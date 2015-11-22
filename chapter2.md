# Instrukcja SELECT

## Wprowadzenie


Instrukcje SQL mogą być wysyłane do bazy danych zarówno wielkimi literami jak i małymi. Nie ma wymagania aby słowa kluczowe (DISTINCT, ORDER, TO_DATE) były pisane wielką literą.


## Podstawy instrukcji SELECT

Instrukcja SELECT pozwala na wybranie rekordów z tabeli lub perspektywy.

SELECT zapewnia funkcje takie jak:

* Projekcja (kolumny)
* Selekcja (wiersze)
* Złączenia (możliwość połączenia więcej niż jednej tabeli)


Podstawowa składnia instrukcji SELECT.

```
SELECT koluna1, kolumna2, ...
FROM tabela
```

Jednym z podstawowych rozszerzeń instrukcji SELECT jest wykorzystanie "*" zamiast listy kolumn, które chcemy wybrać. Wykorzystanie "*" oznacza, że wybieramy wszystkie kolumny z tabeli.

```
SELECT *
FROM tabela

```


#### Przykład 1.1

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

#### Przykład 1.2

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

#### Przykład 1.3

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


#### Zadanie 1.1

Wybierz identyfikator pracownika (kolumna:  EMPLOYEE_ID), identyfikator stanowiska (kolumna: JOB_ID), identyfikator departamentu (kolumna: DEPARTMENT_ID) z tabeli JOB_HISTORY.

#### Zadanie 1.2

Wyświetl całą zawartość tabeli ze stanowiskami (tabela: JOBS)


## DISTINCT

Słowo kluczowe DISTINCT pozwala usunąć duplikaty z rezultatu zwracanego przez instrukcję SELECT.

**UWAGA:** Wykorzystanie DISTINCT na dużej tabeli może mieć negatywny wpływ na wydajność.

#### Przykład 1.4

Wybierz listę wszystkich stanowisk (kolumna: JOB_ID) z tabeli JOB_HISTORY eliminując duplikaty.

```
select distinct job_id
from job_history;
```

Rezultat:

| JOB_ID |
| -- |
| AC_ACCOUNT |
| AC_MGR |
| AD_ASST |
| IT_PROG |
| MK_REP |
| SA_MAN |
| SA_REP |
| ST_CLERK |

DISTINCT może również zostać wykorzystana jeżeli na liście select znajduje się więcej niż jedna kolumna, wtedy przy usuwaniu duplikatów rozważana jest wartość we wszystkich kolumnach.

#### Przykład 1.5

```
select distinct job_id, department_id
from job_history;
```

Rezultat:

JOB_ID|DEPARTMENT_ID
 -- | --
IT_PROG|60
AC_ACCOUNT|90
SA_REP|80
MK_REP|20
SA_MAN|80
AD_ASST|90
AC_ACCOUNT|110
AC_MGR|110
ST_CLERK|50

#### Zadanie 1.3

Wypisz unikalne działy, w których pracują teraz pracownicy, korzystając z tabeli DEPARTMENTS.


#### Zadanie 1.4

Wyświetl unikalne stanowiska (kolumna: JOB_ID) wraz z wysokością pensji (kolumna SALARY z tabeli EMPLOYEES.

## Aliasy

Domyślnie instrukcja SELECT tworzy nagłówki, korzystając z nazw kolumn zdefiniowanych w tabeli.

W bazie danych Oracle istnieje kilka możliwości podania aliasów. Jeżeli alias zawiera biały znak np. spację lub tabulator, należy alias umięścić pomiędzy znakami ". 
Pierwszą z możliwości podania aliasu jest wyspecyfikowanie go po nazwie kolumny w instrukcji SELECT.

#### Przykład 1.6

Wyświetl nazwiska pracowników (kolumna last_name) z tabeli EMPLOYEES. Nadaj kolumnie last_name alias Nazwisko.

```
select last_name Nazwisko
from employees;
```

Rezultat:

| NAZWISKO |
| -- |
| Abel |
| Ande |
| Atkinson |
| Austin |
| Baer |
| ... |


#### Przykład 1.7

Wyświetl nazwiska pracowników (kolumna last_name) z tabeli EMPLOYEES. Nadaj kolumnie last_name alias Nazwisko Pracownika.

```
select last_name "Nazwisko Pracownika"
from employees;
```

Rezultat:

| Nazwisko Pracownika |
| -- |
| Abel |
| Ande |
| Atkinson |
| Austin |
| Baer |
| ... |

Należy zwrócić uwagę, że jeżeli alias nie jest umieszczony pomiędzy znakami ", Oracle zwraca cały alias pisany wielkimi literami. Jeżeli alias umieścimy pomiędzy znakami ", Oracle zachowa wielkość znaków jaką określił programista.

Drugim sposobem określenia aliasu jest wyspecyfikowanie go po słowie kluczowym AS.

```
select kolumna as alias
from tabela;
```

#### Przykład 1.8

Wyświetl identyfikator działu (kolumna: department_id) oraz nazwę działu (kolumna: department_name) oraz nadaj im aliasy numer oraz nazwa dzialu.

```
select department_id as "numer", department_name as "nazwa dzialu"
from departments;
```

Rezultat:

numer|nazwa dzialu
-- | --
10|Administration
20|Marketing
30|Purchasing
40|Human Resources
50|Shipping
60|IT
70|Public Relations
80|Sales
90|Executive
100|Finance
110|Accounting
120|Treasury
130|Corporate Tax
140|Control And Credit
150|Shareholder Services
160|Benefits
170|Manufacturing
180|Construction
190|Contracting
200|Operations
210|IT Support
220|NOC
230|IT Helpdesk
240|Government Sales
250|Retail Sales
260|Recruiting
270|Payroll


#### Zadanie 1.5

Wyświetl wszystkie adresy z tabeli LOCATIONS, nadając poniższym kolumną odpowiednie aliasy. Kolumna STREET_ADDRESS jako Ulica, POSTAL_CODE jako Kod Pocztowy, CITY jako Miasto, COUNTRY_ID jako Panstwo.

#### Zadanie 1.6

Wyświetl kolumnę REGION_NAME, z tabele REGIONS nadajac jej alias NAZWA.


## Tabela DUAL

W bazie Oracle znajduje się tabela DUAL, która zawiera tylko jeden wiersz i pozwala nam konstruować zapytania do obiektów, które nie pochodza z bazy danych. Na przykład do obliczeń numerycznych, lub w celu przetestowania działanie jakiejś funkcji.

#### Przykład 1.9

Oblicz ile sekund jest w dobie.

```
select 60 * 60 * 24
from dual;
```

Rezultat:

| 60 * 60 * 24 |
| -- |
| 86400 |


#### Operatory artmetyczne

| Waga | Operator |  |
| -- | -- | -- |
| 1 | () | Nawiasy |
| 2 | / | Dzielenie |
| 3 | * | Mnożenie |
| 4 | - | Odejmowanie |
| 5 | + | Dodawanie |


#### Zadanie 1.7

Oblicz pole koła o średnicy 4.

#### Zadanie 1.8

Oblicz wartość funkcji y = 2x - 4 dla x = 8. Nadaj wynikowej kolumnie nazwę wynik.

#### Zadanie 1.9

Oblicz wartość y, korzystając z równania
$$y = (x^2 + z^3)/2$$ dla x = 3 oraz z = 5.
Nadaj wynikowej kolumnie nazwę wynik.

### Operatory artmetyczne i daty

W Oracle można wykorzystać operatory + oraz - przy pracy z datami. Jeżeli obydwa argumenty operacji dodawnia lub odejmowania są typu DATE, wynik będzie liczbą dni pomiędzy tymi datami. Jeżeli jednym z operandów jest liczba, jest on traktowany jako liczba dni, a rezultatem bedzie data.

#### Przykład 1.10

Wyświetl ile dni przepracował pracownik (kolumna: EMPLOYEE_ID) na danym stanowsku (kolumna: JOB_ID) korzystając z tabeli JOB_HISTORY, nadając tej kolumnie alias Przepracowanych dni. Data początku pracy znajduje się w kolumnie START_DATE, a zakończenia w kolumnie END_DATE.

```
select employee_id, job_id, 
(end_date - start_date) + 1 "Przepracowanych dni"
from job_history;
```

Rezultat:

EMPLOYEE_ID|JOB_ID|Przepracowanych dni
 -- | -- | --
102|IT_PROG|2019
101|AC_ACCOUNT|1498
101|AC_MGR|1235
201|MK_REP|1402
114|ST_CLERK|648
122|ST_CLERK|365
200|AD_ASST|2101
176|SA_REP|283
176|SA_MAN|365
200|AC_ACCOUNT|1645

#### Zadanie 1.10

Oblicz datę przejścia na emeryturę, zakładając, że trzeba mieć 40 letnią wysługę lat. Jako początek pracy przyjmij kolumnę HIRE_DATE z tabeli EMPLOYEES. Dla uproszczenia przyjmij, że rok ma 365 dni. Wynikowej kolumnie nadaj nazwę Data zakończenia.

## Konkatenacja

Konkatenacja jest to operacja łączenia ze sobą ciągów znaków aby stworzyć nowy ciąg znakowy. Operatorem konkatencji w Oracle Database jest ||.

#### Przykład 1.11

Wyświetl poniższe zdanie dla każdej zany regionu (kolumna: REGION_NAME) zdefiniowanego w tabeli REGIONS:
"nazwa regionu" jest na tabeli Ziemia. 
Nadaj wynikowej kolumnie alias ZDANIE.

```
select region_name || ' jest na planecie Ziemia.' zdanie
from regions;
```

Rezultat:

| ZDANIE |
| -- | 
| Europe jest na planecie Ziemia. |
| Americas jest na planecie Ziemia. |
| Asia jest na planecie Ziemia. |
| Middle East and Africa jest na planecie Ziemia. |

#### Zadanie 1.11

Wypisz swoje imię i nazwisko korzystając z operatora konkatenacji. Nadaj alias nazwa wynikowej kolumnie.


#### Zadanie 1.12

Sporządź dwukolumnowy raport z tabeli EMPLOYEES, w pierwszej kolumnie umieść imię i nazwisko pracownika (kolumny: FIRST_NAME oraz LAST_NAME), a w drugiej jego pobory (kolumna: SALARY). Nadaj alias pierwszej kolumnie Pracownik, a drugiej Pensja.

## Escape'owanie pojedyńczego cudzysłowania

Oracle traktuje wartości umieszczone pomiędzy znakami pojedyńczego cudzysłowia, jako ciągi znakowe. Interesujące jest co się stanie jeżeli ciąg znaków zawiera w sobie pojedyńczy cudzysłów, obrazuje to poniższy przykład.

#### Przykład 1.12

Wyświetl tekst John's book korzystając z tabeli dual.

```
select 'John's book'
from dual;
```

Rezultat:

```
ORA-00923: FROM keyword not found where expected
00923. 00000 -  "FROM keyword not found where expected"
*Cause:    
*Action:
Error at Line: 1 Column: 16
```

Jak widać został zwrócony błąd, gdyż znak ' nie został poprawnie zescape'owany. Jedna z możliwości escape'owania znaku ' w Oracle jest umieszczenie dwóch znaków ' obok siebie.

#### Przykład 1.13

Wyświetl tekst John's book korzystając z tabeli dual Nadaj kolumnie wynikowej alias WYNIK.

```
select 'John''s book' wynik
from dual;
```

Rezultat:

| WYNIK |
| -- |
| John's book |



### Operator q

Operator q jest alternatywną metodą escape'owania znaków w bazie danych Oracle. Pozwala on określić dwa znaki, najczęściej są to pary nawiasów np. [], {}, które poinformują silnik baz danych o tym, żeby potraktował wszystko co jest pomiędzy nimi jako ciąg znaków. Pełna składnia operator q przedstawiona jest poniżej:

```
q'[dowolny diag znaków]'

Przy czym [] jest dowolnym ogranicznikiem tekstu (np. [], {}, ##)
```

Jako ogranicznik tekstu możemy zastosować dowolny jedno bądź wielobajtowy znak za wyjątkiem spacji, tabulatora oraz znaku końca linii. W przypadku wykorzystania nawiaśow stosuje się nawias otwierający i zamykający, w przypadku innych znaków ograniczających powtarza się ten sam znak na końcu i początku tekstu. 

#### Przykład 1.14

Wyświetl tekst John's book korzystając z tabeli dual Nadaj kolumnie wynikowej alias WYNIK. Wykorzystaj operator q.

```
select q'[John's book]' wynik
from dual;
```

Rezultat:

| WYNIK |
| -- |
| John's book |


#### Zadanie 1.13

Wygeneruj nagłówki listów korzystając z tabeli EMPLOYEES, oraz kolumn FIRST_NAME oraz LAST_NAME. Powinna zostać zwrócona jedna kolumna z aliasem Naglowek w formacie: Szanowny Pan'Pani Imię Nazwiski. Wykorzystaj operator q, oraz znak jako ogranicznik tekstu.

## Wartość NULL

W bazach danych występuje specjalna wartość określana jako NULL. NULL oznacza brak wartości. W tabeli każda kolumna, za wyjątkiem tych zdefiniowanych jako klucz głowny, może być zdefiniowana jako przyjmująca wartości NULL lub nie. Najłatwiejszym sposobem na sprawdzenie, do której kolumny możemy przypisać wartości NULL, a do których nie jest użycie polecenia describe na danej tabeli.

#### Przykład 1.14

Sprawdź strukturę tabeli REGIONS.

```
describe regions
```

Rezultat:

Name | Null | Type         
--| -- | --
REGION_ID |  NOT NULL | NUMBER       
REGION_NAME |         | VARCHAR2(25) 


Projektując relacyjną bazę danych należy zawsze zwrócić uwagę na specyfikacje, które kolumny określimy jako akceptujące wartość NULL. Rozważmy poniższy przykład.

```
insert into regions(region_id, region_name) values(99, NULL);
```

Powyższa instrukcja jest poprawna strukturalnie, ale jej wykonanie nie ma większego sensu logicznego, gdyż wstawimy nowy region do tabeli REGIONS. Niestety nowy region nie ma żadnej nazwy, więc jego wykorzystanie w aplikacji jest bardzo wątpliwe.

#### Przykład 1.15 

Wybierz nazwisko (kolumna: LAST_NAME), pensję (kolumna: SALARY) oraz prowizję (kolumna: COMMISSION_PCT) z tabeli EMPLOYEES.

```
select last_name, salary, commission_pct
from employees;
```

Rezultat:

LAST_NAME|SALARY|COMMISSION_PCT
-- | -- | -- 
Davies|3100|
Matos|2600|
Vargas|2500|
Russell|14000|0.4
Partners|13500|0.3
Errazuriz|12000|0.3
Cambrault|11000|0.3
Zlotkey|10500|0.2
Tucker|10000|0.3
Bernstein|9500|0.25
.. | .. | ..

W tym przypadku kolumna COMMISSION_PCT może przyjmować wartości NULL, i ma to sens, gdyż prowizja może być nieokreślona. Alternatywnym rozwiązaniem jest specyfikacja kolumny COMMISSION_PCT jako NOT NULL, wtedy dla wszystkich pracowników, którzy nie mają określonej prowizji, należałoby wstawić wartość 0 w tej kolumnie.

Z wartością NULL związana jest jeszcze jedna istotna właściwość: artmetyczna kalkulacja z wartością NULL, zwraca zawsze NULL.

#### Przykład 1.16

Oblicz pobory pracownika, czyli pensję powiększoną o prowizję.

```
select last_name, salary * commission_pct
from employees;
```

Rezultat:

LAST_NAME | SALARY*COMMISSION_PCT
-- | --
King|
Kochhar|
De Haan|
Hunold|
Rajs|
Davies|
Matos|
Vargas|
Russell|5600
Partners|4050
Errazuriz|3600
Cambrault|3300
Zlotkey|2100
