# Komendy do mysql  

1. **Stworzenie tabelki**  
```sql
CREATE TABLE nazwa_tabelki(cos int itp, cos,);'
```
2. **Wyswietlnenie tabelki**
```sql
SELECT * FROM nazwa_tabelki;
```
3. **Sprawdzenie typu danych w tabeli**
```sql
DESCRIBE nazwa_tabelki;
```
4. **Zeby zmienic wartosc na inna**
```sql
ALTER table nazwa_tabelki ALTER nazwa_kolumny set default 'nazwa';
```
5. **Dodanie kolumny**
```sql
ALTER TABLE nazwa_tabelki ADD COLUMN jaka_kolumne_dodac jakie_ma_wartosci DEFAULT jaki_ma_byc_domyslny;
```
6. **Dodanie do tabelki wartosci**
```sql
INSERT INTO izba (adres_budynku, nazwa_izby, metraz, kolor, wlasciciel) VALUES ('Bajkowa 10', 'Spizarnia2', 10, 'niebieski', (SELECT id_postaci FROM postac WHERE nazwa = 'Tesciowa'));
```
7. **Zmodyfikuj tabelke**
```sql
UPDATE postac SET wiek = 88 WHERE nazwa = 'Tesciowa';
```
