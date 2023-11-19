# Lab04
## Zadanie 1
1. **Stworzenie tabeli postac**
```sql
CREATE TABLE postac (id_postaci INT PRIMARY KEY auto_increment,
nazwa VARCHAR(40),
rodzaj ENUM('wiking', 'ptak', 'kobieta'),
data_ur DATE, wiek INT);
```
2. **Dodanie rekordów do tabeli postac**
```sql
INSERT INTO postac VALUES('Bjorn', 'wiking', '1700-01-01', 323),
('Drozd', 'ptak', '1690-05-15', 332),
('Tesciowa', 'kobieta', '1600-07-20', 423);
```
3. **Zmiana wieku teściowej na 88 lat**
```sql
UPDATE postac SET wiek = 88 WHERE nazwa = 'Tesciowa';
```
## Zadanie 2
1. **Stworzenie tabeli walizka**
```sql
CREATE TABLE walizka (id_walizki INT PRIMARY KEY auto_increment,
pojemnosc INT,
kolor ENUM('rozowy', 'czerwony', 'teczowy', 'zolty'),
id_wlasciciela INT,
FOREIGN KEY (id_wlasciciela) REFERENCES postac(id_postaci) ON DELETE CASCADE);
```
2.**Ustawienie wartosci domyslnej dla koloru**
```sql
ALTER TABLE walizka ALTER COLUMN kolor SET DEFAULT 'rozowy';
```
3. **Dodanie jednej walizki dla Bjorn i Tesciowa**
```sql
INSERT INTO walizka (pojemnosc, id_wlasciciela) VALUES (50, (SELECT id_postaci FROM postac WHERE nazwa = 'Bjorn'));
INSERT INTO walizka (pojemnosc, id_wlasciciela, kolor) VALUES (30, (SELECT id_postaci FROM postac WHERE nazwa = 'Tesciowa'), 'czerwony');
```
## Zadanie 3
1. Stworzenie tabeli izba
```sql
CREATE TABLE izba (
adres_budynku VARCHAR(100) PRIMARY KEY,
nazwa_izby VARCHAR(50) PRIMARY KEY,
metraz INT UNSIGNED,
wlasciciel INT,
FOREIGN KEY (wlasciciel) REFERENCES postac(id_postaci) ON DELETE SET NULL);
```
2. **Dodanie pola kolor po polu metraż**
```sql
ALTER TABLE izba ADD COLUMN kolor VARCHAR(20) DEFAULT 'czarny';
```
3. **Stworzenie izby spiżarnia**
```sql
INSERT INTO izba VALUES ('Bajkowa 3', 'spizarnia', 20, 'zielony', 'Bjorn');
```
## Zadanie 4
1. **Stworzenie tabeli przetwory**
```sql
CREATE TABLE przetwory(
id_przetworu INT PRIMARY KEY auto_increment,
rok_produkcji smallint DEFAULT '1654',
id_wykonawcy INT,
zawartosc VARCHAR(60),
dodatek VARCHAR(60) DEFAULT 'papryczka chili',
id_konsumenta INT,
FOREIGN KEY(id_wykonawcy) REFERENCES postac(id_postac),
FOREIGN KEY(id_konsumenta) REFERENCES postac(id_postac));
```
2. **Wstawienie bigosu z papryczką chilli do tabeli przetwory**
```sql
INSERT INTO przetwory (rok_produkcji, zawartosc) VALUES (2023, 'bigos');
```
## Zadanie 5
1. **Wstawienie 5 wikingów do tabeli postaci**
```sql
INSERT INTO postac (nazwa, rodzaj, wiek) VALUES
('Wiking1', 'wiking', 100),
('Wiking2', 'wiking', 150),
('Wiking3', 'wiking', 400),
('Wiking4', 'wiking', 450),
('Wiking5', 'wiking', 250);
```
2. **Stworzenie tabeli statek**
```sql
CREATE TABLE statek (
nazwa_statku VARCHAR(60) PRIMARY KEY,
rodzaj_statku ENUM('maly', 'sredni', 'duzy'),
data_wodowania DATE,
max_ladownosc INT);
```
3. **Dodanie dwóch statków do tabeli**
```sql
INSERT INTO statek VALUES('Statek1', 'sredni', '1980-02-01', 200), ('Statek2', 'duzy', '1980-01-15', 600)
```
4. **Dodanie pola funkcja do tabeli postac**
```sql
ALTER TABLE postac ADD COLUMN funkcja VARCHAR(60);
```
5. **Zmiana funkcji u Bjorna na kapitan**
```sql
UPDATE postac SET funkcja = 'kapitan' WHERE nazwa = 'Bjorn';
```
6. **Dodanie klucza obcego odwołującego się do statku w tabeli postac**
```sql
ALTER TABLE postac ADD COLUMN statek VARCHAR(60)
ALTER TABLE postac ADD FOREING KEY(statek) references statek (nazwa_statku);
```
7. **Przypisanie wikingów i Drozda do statków**
```sql
UPDATE postac SET statek = 'Statek1' WHERE rodzaj = 'wiking';
UPDATE postac SET statek = 'Statek2' WHERE nazwa = 'Drozd';
```
8. **Usunięcie izby spiżarnia z tabeli izba**
```sql
DELETE FROM izba WHERE nazwa_izby = 'spiżarnia';
```
9. **Usunięcie tabeli izba**
```sql
DROP TABLE izba;
```
