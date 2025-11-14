# SQL-Tworzenie-bazy-danych-definicja-klucza-



Zadanie 1 – Baza danych „Kawiarnia”

Utwórz bazę danych KawiarniaDB zawierającą dwie tabele:

Tabele

Klienci

klient_id (PRIMARY KEY)

imie

nazwisko

email

preferencje

Zamowienia

zamowienie_id (PRIMARY KEY)

klient_id (FOREIGN KEY → Klienci)

data_zamowienia

kwota

Uzupełnij tabele przykładowymi danymi. Następnie wykonaj kwerendy:

Wyświetl wszystkich klientów posortowanych alfabetycznie po nazwisku.

Wyświetl sumę zamówień każdego klienta.

Wyświetl zamówienia o wartości powyżej 30 zł.

Wyświetl klientów, którzy nie mają żadnych zamówień.
