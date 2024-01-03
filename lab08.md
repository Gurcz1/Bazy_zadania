# Lab 8
## Zadanie 1
1.Przekopiuj jeszcze raz z bazy wikingowie rekordy z tabeli kreatura, przekopiuj dodatkowo tabele: uczestnicy, etapy_wyprawy, sektor, wyprawa, wraz z danymi. 
```sql
create table uczestnicy as select * from wikingowie.uczestnicy;
create table etapy_wyprawy as select * from wikingowie.etapy_wyprawy;
create table sektor as select * from wikingowie.sektor;      
create table wyprawa as select * from wikingowie.wyprawa;
```
2. Wypisz nazwy kreatur, które nie uczestniczyły w żadnej wyprawie.
```sql
select k.nazwa from kreatura k  left join wyprawa w on k.idKreatury = w.id_wyprawy where w.id_wyprawy IS null;
```
3. Dla każdej wyprawy wypisać jej nazwę oraz sumę ilości ekwipunku, jaka została zabrana przez
uczestników tej wyprawy.
```sql
select w.nazwa, sum(e.ilosc) from wyprawa w inner join uczestnicy u on w.id_wyprawy = u.id_wyprawy inner join ekwipunek e on u.id_uczestnika =e.idEkwipunku group by w.nazwa;
```
# Zadanie 2
Dla każdej wyprawy wypisz jej nazwę, liczbę uczestników, oraz nazwy tych uczestników w jednej linii.
```sql
SELECT w.nazwa, COUNT(u.id_uczestnika), 
GROUP_CONCAT(p.nazwa ORDER BY p.nazwa ASC SEPARATOR ', ')
FROM wyprawa w left JOIN uczestnicy u ON w.id_wyprawy = u.id_wyprawy left JOIN postac p ON u.id_uczestnika = p.id_postac
GROUP BY w.nazwa;
```
2. Wypisz kolejne etaty wszystkich wypraw wraz z nazwami sektorów, sortując najpierw według daty początku wyprawy, a następnie według kolejności występowania etapów. W każdym etapie określ nazwę kierownika danej wyprawy.
```sql
select w.id_wyprawy, ew.sektor, s.nazwa, ew.kolejnosc, w.data_rozpoczecia, k.nazwa from etapy_wyprawy ew inner join sektor s on ew.sektor = s.id_sektora 
inner join wyprawa w on w.id_wyprawy = ew.idWyprawy 
inner join kreatura k on k.idKreatury =w.kierownik
order by w.data_rozpoczecia asc, ew.kolejnosc asc;
```
# Zadanie 3 
1. Wypisać ile razy dany sektor był odwiedzany podczas wszystkich wypraw (nazwa sektora, ilość odwiedzin). Jeśli nie był odwiedzony ani razu, wpisz zero.
```sql
select s.nazwa, count(ew.sektor) from sektor s left join etapy_wyprawy ew on s.id_sektora = ew.sektor group by s.nazwa;
```
2.W zależności od ilości wypraw, w jakich brała udział dana kreatura wypisz: nazwa kreatury, 'brał udział w wyprawie' - gdy liczba > 0, 'nie brał udziału w wyprawie', gdy równa zero.
```sql
select k.nazwa, if(count(u.id_uczestnika)>0,'bral udzial','nie bral udzialu') from uczestnicy u right join kreatura k on k.idKreatury=u.id_uczestnika group by k.nazwa;
```
# Zadanie 4
1.
```sql
SELECT w.nazwa , SUM(LENGTH(e.dziennik)) AS SumaZnakowDziennika FROM wyprawa w
INNER JOIN etapy_wyprawy e ON w.id_wyprawy = e.idWyprawy
GROUP BY w.id_wyprawy, w.nazwa
HAVING SumaZnakowDziennika < 400 OR SumaZnakowDziennika IS NULL;
```
2.
```sql
SELECT w.nazwa, SUM(e.ilosc * z.waga) / COUNT(u.id_uczestnika) FROM wyprawa w
INNER JOIN uczestnicy u ON w.id_wyprawy = u.id_wyprawy
INNER JOIN ekwipunek e ON u.id_uczestnika = e.idKreatury
INNEr JOIN zasob z ON e.idZasobu = z.idZasobu
GROUP BY w.id_wyprawy, w.nazwa;
```
# Zadanie 5
```sql
select w.nazwa, k.nazwa, datediff(w.data_rozpoczecia,k.dataUr) from kreatura k inner join uczestnicy u on u.id_uczestnika=k.idKreatury
inner join wyprawa w on u.id_wyprawy = w.id_wyprawy
inner join etapy_wyprawy ew on ew.idWyprawy=w.id_wyprawy
where ew.sektor=7 group by w.id_wyprawy, k.idKreatury;
```
