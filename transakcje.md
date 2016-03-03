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


