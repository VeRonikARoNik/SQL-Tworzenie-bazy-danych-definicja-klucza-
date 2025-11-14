# Zadanie – SQL: Tworzenie bazy danych, klucz główny i klucz obcy

I

## Opis zadania

### Zadanie polega na zaprojektowaniu prostej relacyjnej bazy danych przedstawiającej system zamówień w kawiarni. Celem ćwiczenia jest zrozumienie, jak działają klucz główny (PRIMARY KEY) oraz klucz obcy (FOREIGN KEY) oraz jak tworzy się relację typu jeden-do-wielu między tabelami. 

## Treść zadania

1. Utwórz bazę danych o nazwie KawiarniaDB.
2. Utwórz w niej dwie tabele:
2. Utwórz w niej dwie tabele:

Tabela: Klienci
Zawiera informacje o klientach.

Pola:

  klient_id — klucz główny (PRIMARY KEY)
  imie
  nazwisko
  email
  preferencje

Tabela: Zamowienia
Zawiera informacje o zamówieniach złożonych przez klientów.

Pola:
zamowienie_id — klucz główny (PRIMARY KEY)
klient_id — klucz obcy (FOREIGN KEY) wskazujący na klient_id w tabeli Klienci
data_zamowienia
kwota

Relacja: jeden klient może mieć wiele zamówień.

3. Wstaw dane przykładowe

Minimum 4 klientów

Minimum 4 zamówienia powiązane z klientami

4. Wykonaj i zapisz poniższe kwerendy SQL:

Wyświetl wszystkich klientów posortowanych alfabetycznie po nazwisku.

Wyświetl sumę zamówień wykonanych przez każdego klienta.

Wyświetl zamówienia o wartości większej niż 30 zł.

Wyświetl klientów, którzy nie mają żadnych zamówień.

```
-- ============================================================
-- 1. UTWORZENIE BAZY DANYCH
-- ============================================================

CREATE DATABASE KawiarniaDB;
USE KawiarniaDB;

-- ============================================================
-- 2. TWORZENIE TABEL
-- ============================================================

CREATE TABLE Klienci (
    klient_id INT PRIMARY KEY,
    imie VARCHAR(50),
    nazwisko VARCHAR(50),
    email VARCHAR(100),
    preferencje VARCHAR(150)
);

CREATE TABLE Zamowienia (
    zamowienie_id INT PRIMARY KEY,
    klient_id INT,
    data_zamowienia DATE,
    kwota DECIMAL(6,2),
    FOREIGN KEY (klient_id) REFERENCES Klienci(klient_id)
);

-- ============================================================
-- 3. WSTAWIANIE PRZYKŁADOWYCH DANYCH
-- ============================================================

INSERT INTO Klienci VALUES
(1, 'Anna', 'Kowalska', 'anna.kowalska@gmail.com', 'Latte, Ciasto'),
(2, 'Jan', 'Nowak', 'jan.nowak@gmail.com', 'Czarna kawa'),
(3, 'Maria', 'Zielińska', 'm.zielinska@gmail.com', 'Herbata, Cappuccino'),
(4, 'Piotr', 'Lewandowski', 'piotr.lew@gmail.com', 'Espresso');

INSERT INTO Zamowienia VALUES
(1, 1, '2025-01-10', 25.50),
(2, 1, '2025-01-15', 32.00),
(3, 2, '2025-01-11', 12.00),
(4, 3, '2025-01-20', 44.99);

-- ============================================================
-- 4. KWERENDY DO WYKONANIA
-- ============================================================

-- 1. Wyświetl wszystkich klientów posortowanych alfabetycznie po nazwisku
SELECT * FROM Klienci ORDER BY nazwisko;

-- 2. Wyświetl sumę zamówień każdego klienta
SELECT 
    k.imie, 
    k.nazwisko, 
    SUM(z.kwota) AS suma_zamowien
FROM Klienci k
LEFT JOIN Zamowienia z ON k.klient_id = z.klient_id
GROUP BY k.klient_id;

-- 3. Wyświetl zamówienia o wartości powyżej 30 zł
SELECT * FROM Zamowienia WHERE kwota > 30;

-- 4. Wyświetl klientów, którzy nie mają żadnych zamówień
SELECT k.*
FROM Klienci k
LEFT JOIN Zamowienia z ON k.klient_id = z.klient_id
WHERE z.zamowienie_id IS NULL;

```
II

Zadanie 2 – SQL: Wypożyczalnia Filmów
Treść zadania

Utwórz bazę danych FilmyDB zawierającą dwie tabele:

Tabela: Filmy

film_id — PRIMARY KEY
tytul
gatunek
rok_produkcji

Tabela: Wypozyczenia
wypozyczenie_id — PRIMARY KEY
film_id — FOREIGN KEY → Filmy
data_wypozyczenia
data_zwrotu (może być NULL)

Wstaw dane:
minimum 5 filmów,
minimum 4 wypożyczenia.

Wykonaj kwerendy:

Wyświetl wszystkie filmy z gatunku "Sci-Fi".

Wyświetl filmy, które nigdy nie były wypożyczone.

Wyświetl filmy wypożyczone więcej niż 1 raz.

Wyświetl filmy, które są aktualnie wypożyczone (data_zwrotu = NULL).

III

Zadanie 3 – SQL: Szkoła Muzyczna
Treść zadania

Utwórz bazę danych MuzykaDB, która przechowuje informacje o uczniach i ich lekcjach.

Tabela: Uczniowie

uczen_id — PRIMARY KEY

imie

nazwisko

instrument

Tabela: Lekcje

lekcja_id — PRIMARY KEY

uczen_id — FOREIGN KEY → Uczniowie

data_lekcji

czas_trwania_min

Wstaw dane:

minimum 4 uczniów,

minimum 4 lekcje.

Wykonaj kwerendy:

Wyświetl wszystkich uczniów grających na pianinie.

Wyświetl liczbę lekcji każdego ucznia.

Wyświetl uczniów, którzy mieli lekcję w ostatnich 30 dni.

Wyświetl średni czas lekcji dla każdego instrumentu.
