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

Po uruchomieniu SQL * Plus podajemy polecenia w prompt'cie SQL * Plus'a, który domyślnie jest oznaczony jako *SQL>*. W celu zamknięcia SQL*Plus'a możemy wykorzystać polecenia quit lub exit.

W SQL*Plus każde polecenie należy zakończyć znakiem terminatora: „;” lub „/” w nowej linni.