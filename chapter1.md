# Wprowadzenie do narzędzi w Oracle

Dwoma najczęściej stosowanymi narzędziami do obsługi Oracle są SQL*Plus oraz SQLDeveloper.

## SQL*Plus

SQL*Plus jest narzędziem działającym w lini poleceń. Jest to podstawowe narzędzie wykorzystywane przez administratorów bazy danych, stosowane jest również przez programistów. 

W SQL*Plus istnieją dwa podstawowe sposoby podłączenia się do bazy danych.

Pierwszym jest podanie specyfikacji połączenia podczas uruchomienie SQL*Plus'a

```
sqlplus urzytkownik/haslo@net-service-name
```

Jeżeli jesteśmy zalogowanie na serwerze, na którym jest zainstalowana baza danych i jest ustawiona zmienna środowiskowa ORACLE_SID, @net-service-name można pominąć, gdyż Oracle wykorzystuje wtedy IPC (Inter Process Communication).

#### Przykład 0.1

Połącz się z lokalną bazą danych korzystając SQL*Plus.

```
sqlplus hr/hr
SQL>quit
```

#### Przykład 0.2

Połącz się z bazą danych korzystając z SQL*Plus i orcl jako Net Service Name.

```
sqlplus hr/hr@orcl
SQL>exit
```

Po uruchomieniu SQL*Plus podajemy polecenia w prompt'cie SQL*Plus'a, który domyślnie jest oznaczony jako *SQL>*. W celu zamknięcia SQL*Plus'a możemy wykorzystać polecenia quit lub exit.

Drugim sposobem połączenia się z bazą danych korzystając z SQL*Plus, jest uruchomienie SQL*Plus'a bez podawania specyfikacji połączenia. Następnie wykorzystujemy polecenie CONNECT. Polecenie CONNECT wymaga podania takies samej specyfikacji połączenia jak podawana podczas uruchomienia SQLPlus'a.

#### Przykład 0.3

Uruchom narzędzie SQL*Plus bez logowania się do bazy danych, a następnie połącz się do bazy danych, korzystając z polecenia CONNECT.

```
sqlplus /nolog

SQL> connect hr/hr

Connected.
```

#### Przykład 0.4

Uruchom narzędzie SQL*Plus bez logowania się do bazy danych, a następnie połącz się do bazy danych wykorzystując net service name orcl, korzystając z polecenia CONNECT.

```
sqlplus /nolog

SQL> connect hr/hr@orcl

Connected.
```

W SQL*Plus każdą instrukcje SQL należy zakończyć znakiem terminatora: „;” lub „/” w nowej linni.

#### Przykład 0.5

Wyświetl nazwy tabel znajdujące się w schemacie użytkownika hr.

```
SQL> select table_name
  2  from user_tables
  3  /

TABLE_NAME
------------------------------
LOCATIONS
COUNTRIES
JOB_HISTORY
REGIONS
DEPARTMENTS
EMPLOYEES
JOBS
```

Alternatywnie możemy wykorzystać średnik aby zakończyć instrukcję SQL.

```
SQL> select table_name
  2  from user_tables;

TABLE_NAME
------------------------------
LOCATIONS
COUNTRIES
JOB_HISTORY
REGIONS
DEPARTMENTS
EMPLOYEES
JOBS

7 rows selected.
```

## SQL Developer

SQL Developer jest narzędziem GUI, wykorzystywanym głównie do programowania baz danych.

#### Przykład 0.6

Połącz się do bazy danych korzystając z SQL Developer'a.


