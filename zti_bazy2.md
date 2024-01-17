# Lab 3. Zadania część 2
## Zadanie 1
## Wyświetl nazwę działu i minimalną, maksymalną i średnią wartość pensji w każdym dziale.
```sql
select d.nazwa,max(pensja),min(pensja),avg(pensja) from dzial d
inner join pracownik p on d.id_dzialu=p.dzial group by d.id_dzialu;
```
## Zadanie 2
## Wyświetl pełną nazwę klienta, wartość zamówienia dla 10 najwyższych wartości zamówienia.
```sql
select k.pelna_nazwa,sum(pz.ilosc*pz.cena) as sumazamowienia, z.id_zamowienia from klient k
inner join zamowienie z on k.id_klienta=z.klient 
inner join pozycja_zamowienia pz on pz.zamowienie=z.id_zamowienia
group by z.id_zamowienia order by sumazamowienia desc limit 10;
```
## Zadanie 3
## Wyświetl wartość przychodu dla każdego roku. Dane posortuj malejąco według sumy wartości zamówień.
```sql
select year(z.data_zamowienia) as rok,sum(pz.ilosc*cena) as przychod from zamowienie z
inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
inner join towar t on pz.towar=t.id_towaru group by rok order by przychod;
```
## Zadanie 4
## Wyświetl sumę wartości wszystkich anulowanych zamówień.
```sql
select sum(pz.ilosc*pz.cena) from zamowienie z
inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
where status_zamowienia = 6 group by z.id_zamowienia;
```
## Zadanie 5
## Wyświetl liczbę zamówień i sumę zamówień dla każdego miasta z podstawowego adresu klientów.
```sql
select ak.miejscowosc, count(z.id_zamowienia) from adres_klienta ak
inner join klient k on k.id_klienta=ak.klient 
inner join zamowienie z on z.klient=k.id_klienta
inner join pozycja_zamowienia pz on pz.zamowienie=z.id_zamowienia 
group by ak.miejscowosc;
```
## Zadanie 6
## Wyświetl dotychczasowy dochód firmy biorąc pod uwagę tylko zamówienia zrealizowane.
```sql
select sum(pz.ilosc*cena) as przychod from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
inner join towar t on pz.towar=t.id_towaru where z.status_zamowienia = 5;
```
## Zadanie 7
## Policz i wyświetl dochód (przychód z zamówień i cena zakupu towaru) w każdym roku działalności firmy.
```sql
select year(z.data_zamowienia) as rok,sum((pz.ilosc*cena)-(pz.ilosc*t.cena_zakupu)) as przychod from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
inner join towar t on pz.towar=t.id_towaru group by rok order by przychod;
```
## Zadanie 8
## Wyświetl wartość aktualnego stanu magazynowego z podziałem na kategorię produktów.
```sql
select nazwa_kategori,sum(ilosc) from stan_magazynowy sm inner join towar t on t.id_towaru=sm.towar 
inner join kategoria k on k.id_kategori=t.kategoria group by kategoria;
```
## Zadanie 9
## Przygotuj zapytanie, które wyświetli dane w poniższej postaci (policz ilu pracowników urodziło się w danym miesiącu - uwaga na porządek sortowania).
```sql
select monthname(data_urodzenia) as miesiacur, count(id_pracownika)
from pracownik group by miesiacur order by month(data_urodzenia);
```
# Zadanie 10
select * from pracownik;
