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