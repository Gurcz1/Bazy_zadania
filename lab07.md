# Lab 7
## Zadanie 1
 1. wyświetl średnią wagę wszystkich wikingów
```sql
select avg(waga) as srd_waga from kreatura where rodzaj = 'wiking';
```
2. Wyświetl średnią wagę oraz liczbę kreatur dla każdego rodzaju
```sql
select rodzaj, avg(waga), count(*) from kreatura group by rodzaj;
```
3. wyświetl średni wiek dla każdego rodzaju kreatury
```sql
select avg('2023'-year(dataUr)) from kreatura group by rodzaj;
```
# Zadanie 2
1. Dla każdego rodzaju zasobu wyświetlić sumę wag tego zasobu.
``sql
select rodzaj ,sum(waga) from zasob group by rodzaj;
```  
2. Dla każdej nazwy zasobu wyświetlić średnią wagę, jeśli ilość jest równa co najmniej 4 oraz
jeśli ta suma wag jest większa od 10.
```sql
select sum(waga) from zasob where ilosc > 4 group by rodzaj having sum(waga) > 5;
```
3. Wyświetlić ile jest różnych nazw dla każdego rodzaju zasobu, jeśli minimalna liczba zasobu
jest większa od 1.
```sql
select rodzaj, count(distinct nazwa) from zasob where ilosc > 1 group by rodzaj;
```
# Zadanie 3
1. Wyświetlić dla każdej kreatury ilości zasobów jakie niesie
```sql
select k.nazwa, e.ilosc from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu;
```
2. Wyświetlić dla każdej kreatury nazwy zasobów jakie posiada.
```sql
select k.nazwa, z.nazwa from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu;
```
3. Wyświetlić kreatury, które nie posiadają żadnego ekwipunku.
```sql
select k.nazwa, e.idZasobu, e.ilosc from kreatura k left join ekwipunek e on k.idKreatury=e.idKreatury where e.idKreatury is null;
```
# Zadanie 4
1. Wyświetlić nazwy wikingów, którzy urodzili się w latach 70-tych XVII wieku oraz nazwy
zasobów, które posiadają (użyj natural joina jeśli się da).
```sql
SELECT k.nazwa, z.nazwa, k.dataUr FROM kreatura k JOIN zasob z ON k.idKreatury = z.idZasobu WHERE YEAR(k.dataUr) BETWEEN 1600 AND 1699 and k.rodzaj = 'wiking';
```
2. Wyświetlić nazwy 5 najmłodszych kreatur, które w ekwipunku posiadają jedzenie.
```sql
select k.nazwa, k.dataUr, z.rodzaj from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu where z.rodzaj='jedzenie' order by k.dataUr desc limit 5;
```
3. Wypisz obok siebie nazwy kreatur, których numer idKreatury różni się o 5 (np. Bjorn - Astrid,
Brutal - Ibra itd.).
```sql
select concat(k2.nazwa, '-', k1.nazwa) from kreatura k1 inner join kreatura k2 on k1.idkreatury-k2.idKreatury = 5;
```
# Zadanie 5
1. Dla każdego rodzaju kreatury wyświetlić średnią wagę zasobów, jaką posiadają w ekwipunku, jeśli kreatura nie jest małpą ani wężem i ilość ekwipunku jest poniżej 30
```sql
select k.rodzaj, avg(e.ilosc * z.waga) from kreatura k inner join ekwipunek e on k.idKreatury= e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu 
where k.rodzaj not in ('malpa','waz') and e.ilosc < 30 group by k.rodzaj ;
```
2. Dla każdego rodzaju kreatury wyświetlić nazwę, datę urodzenia i rodzaj najmłodszej i najstarszej kreatury
```sql
select k.rodzaj,k.nazwa, n.najstarsza, n.najmlodsza from (select rodzaj, min(dataUr) najstarsza,  max(dataUr) najmlodsza from kreatura group by rodzaj) n, kreatura k 
where n.najstarsza=k.dataUr or n.najmlodsza=k.dataUr;
```
