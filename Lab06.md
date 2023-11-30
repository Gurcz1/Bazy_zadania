# Lab06
## Zadanie 1
1. Skopiuj tabele 'kreatura','zasob','ekwipunek' z bazy 'wikingowie' do swojej bazy
```sql
create table kreatura as select * from wikingowie.kreatura;
create table zasob as select * from wikingowie.zasob;
create table ekwipunek as select * from wikingowie.ekwipunek;
```
2. Wypisz wszystkie rekordy z tabeli 'zasob'.
```sql
select * from zasob;
```
3. Wypisz wszystkie rekordy z tabeli 'zasob' gdzie typ to jedzenie.
```sql
select * from zasob where rodzaj = 'jedzenie';
```
## Zadanie 2
1. Wyświetl kreatury, które nie są wiedźmą i dźwigają co najmniej 50kg.
```sql
select * from kreatura where rodzaj != 'wiedzma' and udzwig >= 50;
```
2. Wyświetl zasoby, które ważą pomiędzy 2 a 5 kg.
```sql
select * from zasob where waga between 2 and 5;
```
3. Wyświetl kreatury, których nazwa zawiera 'or' i które dźwigają między 30kg a 70kg.
```sql
select * from kreatura where nazwa like '%or%' and udzwig between 30 and 70;
```
# Zadanie 3
1. Wyświetl zasoby, które zostały pozyskane w miesiącach lipcu i sierpniu. 
```sql
select * from zasob where month(dataPozyskania) between 7 and 8;
```
2. Wyświetl zasoby, które mają zdefiniowany rodzaj od najlżejszego do najcięższego. 
```sql
select * from zasob order by waga asc;
```
3. Wyświetl 5 najstarszych kreatur.
```sql
select * from kreatura where dataUr is not null order by dataUr asc limit 5;
```
# Zadanie 4
1. Wyświetl unikalne rodzaje zasobów. 
```sql
select distinct rodzaj from zasob;
```
2. Wyświetl jako jedną kolumnę nazwę i rodzaj kreatury (w postaci: nazwa - rodzaj), gdzie rodzaj rozpoczyna się od 'wi'.
```sql
select concat(nazwa,'-', rodzaj) from kreatura where rodzaj like '%wi%';
```
3. Wyświetl zasoby z całkowitą wagą danego zasobu (ilość * waga) dla zasobów pozyskanych w latach 2000-2007.
```sql
select concat(nazwa, ' ' ,ilosc*waga) as calkowaita_waga from zasob where year(dataPozyskania) between 2000 and 2007;
```
# Zadanie 5
1. Zakładając, że każdy rodzaj jedzenia to 30% odpadu, wyświetl masę właściwego jedzenia (netto) oraz wagę odpadków.
```sql
select idZasobu, nazwa, ilosc, dataPozyskania, waga, waga*0.7 as 'wlasciwa waga', waga * 0.3 as 'masa odpadkow', rodzaj from zasob;
```
2. Wyświetl zasoby, które nie mają rodzaju.
```sql
select * from zasob where rodzaj is null;
```
3. Wyświetl wszystkie unikalne rodzaje zasobów, których nazwa zaczyna się od 'Ba' lub kończy się na 'os'. Dane posortuj alfabetycznie.
```sql
select distinct rodzaj from zasob where nazwa like 'Ba%' or nazwa like '%os' order by rodzaj asc;
```
