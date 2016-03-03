# Transakcje

## ACID

Istnieją cztery wymagania jakie stawia się przed systemami relacyjnych baz danych co do współbieżnego wykonywania transakcji. Są to:

* A - Atomicity (atomowość)
* C - Consitency (spójność)
* I - Isolation (izolacja)
* D - Durability (trwałość)

**Atomowość** - każda transakcja jest niepodzielną operacją z punktu widzenia użytkownika: albo wszystkie akcje wchodzące w skład transakcji są wykonywane albo żadna z nich.

**Spójność** - po wykonaniu zbioru transakcji stan bazy danych powinien być spójny (pod warunkiem, że przy rozpoczynaniu transakcji stan bazy danych był spójny oraz że każda z wykonywanych transakcji jest z osobna poprawna).

**Izolacja** - transakcje powinny sobie wzajemnie nie  przeszkadzać w działaniu. Każdy użytkownik powinien mieć iluzję, że sam korzysta z bazy danych.

**Trwałość** - dane zatwierdzone przez transakcję powinny być dostępne nawet w sytuacji awarii programu, komputera lub nośnika danych.

Baza danych stosuje poniższe metody, aby spełnić aksjomaty ACID:

* Blokady (locks) zakładane na obiekty – ograniczające albo wręcz uniemożliwiające działanie innych transakcji na zablokowanym obiekcie.

* Dziennik (redo log / transactional log) zapisywanie wszystkich zmian w bazie danych do specjalnego dziennika (logu), aby w razie potrzeby móc: dla nie zatwierdzonej transakcji wycofać wprowadzone przez nią zmiany, w przypadku awarii odtworzyć spójny stan bazy danych.

* Kopia zabezpieczająca (backup) - wykonywana w regularnych odstępach czasu, na przykład raz na dzień; w przypadku awarii danych na dysku pozwala przywrócić spójny stan bazy danych.

* Wielowersyjność - możliwość odczytywania danych zmienianych równocześnie przez inne transakcje w takiej postaci w jakiej istniały w pewnych chwilach w przeszłości (np. w chwili rozpoczynania się danego zapytania lub danej transakcji).


## Atomowość

Atomowość transakcji

Transakcja może zakończyć swoje działanie na cztery sposoby:

* zatwierdzeniem (COMMIT) po zakończeniu wszystkich swoich akcji,
* wycofaniem (ROLLBACK) - anulowaniem wszystkich wykonanych akcji,
* może zostać przerwana przez silnik bazy danych (abort), a następnie wycofana (np. z powodu zakleszczenia - deadlock),
* zanim dojdzie do końca może zostać przerwana z powodu awarii serwera lub dysku - po podniesieniu systemu po awarii dotychczasowe zmiany wprowadzone przez transakcję zostają na chwilę przywrócone a następnie wycofane przez system (ponieważ transakcja nie zakończyła się zatwierdzeniem).
W każdej więc z tych sytuacji albo cała transakcja zostaje wykonana albo żadna jej część nie zostaje wykonana. Transakcję można traktować jak pojedynczą, atomową operację na bazie danych.

### Przykład

Wykonanie transferu 100 złotych pomiędzy kontami. Jeżeli serwer będzie miał awarię po pierwszej instrukcji update, wynik będzie niepoprawny z logicznego punktu widzenia.

```
update konta set saldo = saldo - 100 where id = 1;
commit;
-- tutaj następuje awaria
update konta set saldo = saldo + 100 where id = 2;
commit;
```
Poprawnie zaprogramowana transakcja powinna wyglądać tak.

```
update konta set saldo = saldo - 100 where id = 1;
update konta set saldo = saldo + 100 where id = 2;
commit;
```


## Spójność

Ta właściwość gwarantuje, że baza będzie w spójnym stanie bez względu na to czy transakcja się powiodła czy nie.

### Przykład

```
create table wykladowcy(
id number(6,0) primary key,
nazwisko varchar2(64) not null);

create table grupy(
id number(8,0) primary key,
nazwa varchar2(64) not null,
wykladowca_id number(6,0) not null);

alter table grupy add constraint grupy_wykladowcy_fk
foreign key (wykladowca_id) references wykladowcy(id);

insert into wykladowcy values(1,'Kowalski');

insert into grupy(id, nazwa, wykladowca_id) values(101,'101/2015', 1);

commit;


insert into grupy(id, nazwa, wykladowca_id) values(102,'102/2015', 2);
insert into grupy(id, nazwa, wykladowca_id) values(102,'102/2015', 2)
*
ERROR at line 1:
ORA-02291: integrity constraint (HR.GRUPY_WYKLADOWCY_FK) violated - parent key
not found
```

Jak widać baza danych nie pozwoliła utworzyć rekordu w tabeli grupy, bez przypisania istniejącego wykładowcy.


## Izolacja

Do zobrazowania izolacji wykorzystamy dwie sesje, oznaczone jako S1 oraz S2

```
S1:
SQL> select* from wykladowcy;

        ID NAZWISKO
---------- ----------------------
         1 Kowalski
         
SQL> insert into wykladowcy values(2, 'Wisniewski');

1 row created.

SQL> select * from wykladowcy;

        ID NAZWISKO
---------- -------------------------------------------
         1 Kowalski
         2 Wisniewski
 
 S2:
 SQL> select * from wykladowcy;

        ID NAZWISKO
---------- ------------------------
         1 Kowalski
         
Jak widać inne sesje nie widzi niezatwierdzonych danych.

S1:

SQL> commit;

Commit complete.

S2:

SQL> select * from wykladowcy;

        ID NAZWISKO
---------- ------------------------
         1 Kowalski
         2 Wisniewski
         
Dopiero po zatwierdzeniu transakcji przez S1, sesja S2 widzi zatwierdzone dane.

```

