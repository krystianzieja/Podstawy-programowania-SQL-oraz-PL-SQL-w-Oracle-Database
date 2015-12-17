# Operatory zbiorowe

W Oracle występują cztery operatory zbiorowe. Wykorzystujemy je do pracy ze "złożonymi kwerendami", czyli kwerendami, które zawierają więcej niż jedną instrukcję SELECT.

Operator | Znaczenie
-- | -- 
UNION | Zwraca wiersze z obydwu kwerend, eliminujać duplikaty
UNION ALL | Zwraca wiersze z obydwu kwerend , nie eliminując duplikatów
INTERSECT | Zwraca wiersze, które występują w obydwu kwerendach
MINUS | Zwraca wiersze z pierwszej kwerendy, któe nie występują w drugiej kwerendzie

Wszystkie powyższe operatory mają taką samą ważność, co powoduje, że Oracle je rozpatruje od góry do dołu zgodnie z miejscem występowania w kwerendzie.

Liczba wyrażeń na listach SELECT musi być taka sama.

Typ danych kolumn w drugiej kwerendzie musi odpowiadać pierwszej kwerendzie.

Możmy wykorzystać nawiasy, aby zmienić koleność wykonania kwerend.

Klauzula ORDER BY może być użyta tylko na samym końcu całej instrukcji.



