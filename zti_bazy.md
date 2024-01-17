Zadanie 1

Wyświetl imię i nazwisko każdego pracownika i jego rok urodzenia.
```sql
select imie, nazwisko, year(data_urodzenia) from pracownik;
```
Zadanie 2
Wyświetl imię i nazwisko pracowników oraz ich wiek w latach (bez uwzględniania miesiąca i dnia urodzenia).
```sql
select imie, nazwisko, '2024'-year(data_urodzenia) as wiek from pracownik;
```
Zadanie 3
Wyświetl nazwę działu i liczbę pracowników przypisanych do każdego z nich.
```sql
select d.nazwa, count(d.id_dzialu) from dzial d inner join pracownik p on d.id_dzialu=p.dzial group by d.nazwa;  
```
Zadanie 4
Wyświetl nazwę kategorii oraz liczbę produktów w każdej z nich
```sql
select k.nazwa_kategori, sum(pz.ilosc) from kategoria k
inner join towar t on t.kategoria=k.id_kategori
inner join pozycja_zamowienia pz on pz.towar= t.id_towaru group by k.nazwa_kategori;
```
Zadanie 5
Wyświetl nazwę kategorii i w kolejnej kolumnie listę wszystkich produktów należącej do każdej z nich.
```sql
select k.nazwa_kategori,group_concat(t.nazwa_towaru) from kategoria k
inner join towar t on t.kategoria=k.id_kategori group by k.nazwa_kategori;
```
Zadanie 6
Wyświetl średnie zarobki pracowników za zaokrągleniem do 2 miejsc po przecinku.
```sql
select round(avg(pensja),2) from pracownik;
```
Zadanie 7
Wyświetl średnie zarobki pracowników, którzy pracują co najmniej od 5 lat.
```sql
select * from pracownik where data_zatrudnienia < '2019-01-11';
```
Zadanie 8
Wyświetl 10 najczęściej sprzedawanych produktów.
```sql
select sum(pz.ilosc), t.nazwa_towaru from pozycja_zamowienia pz
inner join towar t on pz.towar=t.id_towaru group by pz.towar order by sum(pz.ilosc) desc limit 10;
```
Zadanie 9
Wyświetl numer zamówienia, jego wartość (suma wartości wszystkich jego pozycji) zarejestrowanych w pierwszym kwartale 2017 roku.
```sql
select z.numer_zamowienia, sum(pz.cena*pz.cena), z.data_zamowienia from zamowienie z
inner join pozycja_zamowienia pz on pz.zamowienie=z.id_zamowienia group by z.id_zamowienia
having date(z.data_zamowienia) between '2017-01-01' and '2017-03-31';
```
Zadanie 10
Wyświetl imie, nazwisko i sumę wartości zamówień, które dany pracownik dodał. Posortuj malejąco po sumie.
```sql
select sum(pz.cena*pz.cena) as wartosc, p.imie,p.nazwisko from zamowienie z inner join pozycja_zamowienia pz on pz.zamowienie=z.id_zamowienia
inner join pracownik p on p.id_pracownika=z.pracownik_id_pracownika group by p.id_pracownika order by wartosc desc;
```
