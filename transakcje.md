# Transakcje

## ACID

Istnieją cztery wymagania jakie stawia się przed systemami relacyjnych baz danych co do współbieżnego wykonywania transakcji. Są to:

* A - Atomicity (atomowość)
* C - Consitency (spójność)
* I - Isolation (izolacja)
* D - Durability (trwałość)

**Atomowość** - każda transakcja jest niepodzielną operacją z punktu widzenia użytkownika: albo wszystkie akcje wchodzące w skład transakcji są wykonywane albo żadna z nich.

**Spójność** - po wykonaniu zbioru transakcji stan bazy danych powinien być spójny (pod warunkiem, że przy rozpoczynaniu transakcji stan bazy danych był spójny oraz że każda z wykonywanych transakcji jest z osobna poprawna).

