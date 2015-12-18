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

```