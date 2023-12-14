select avg(waga) as srd_waga from kreatura where rodzaj = 'wiking';
select rodzaj, avg(waga), count(*) from kreatura group by rodzaj;
select * from kreatura; 
select avg('2023'-year(dataUr)) from kreatura group by rodzaj;
select rodzaj ,sum(waga) from zasob group by rodzaj;
select * from zasob;
select sum(waga) from zasob where ilosc > 4 group by rodzaj having sum(waga) > 5;
select rodzaj, count(distinct nazwa) from zasob where ilosc > 1 group by rodzaj;
select nazwa, avg(waga) from zasob where ilosc >= 4 group by nazwa having sum(waga) > 10;
select * from kreatura, ekwipunek where kreatura.idKreatury=ekwipunek.idKreatury;
select * from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury;
select k.nazwa, e.idZasobu, e.ilosc from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu;
select k.nazwa, e.idZasobu, e.ilosc from kreatura k left join ekwipunek e on k.idKreatury=e.idKreatury where e.idKreatury is null;
select distinct idKreatury from ekwipunek;
select nazwa, idKreatury from kreatura where idKreatury not in (select distinct idKreatury from ekwipunek where idKreatury is not null);
select * from kreatura natural join ekwipunek;
select k.nazwa, k.dataUr, z.rodzaj from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu where z.rodzaj='jedzenie' order by k.dataUr desc limit 5;
select concat(nazwa, nazwa) from kreatura;
select k.nazwa, k.dataUr, z.rodzaj from kreatura k inner join ekwipunek e on k.idKreatury= e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu 
where z.rodzaj='jedzenie' order by k.dataUr desc limit 5;
select concat(k2.nazwa, '-', k1.nazwa) from kreatura k1 inner join kreatura k2 on k1.idkreatury-k2.idKreatury = 5;
select k.rodzaj, avg(e.ilosc * z.waga) from kreatura k inner join ekwipunek e on k.idKreatury= e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu 
where k.rodzaj not in ('malpa','waz') and e.ilosc < 30 group by k.rodzaj ;

select k.rodzaj,k.nazwa, n.najstarsza, n.najmlodsza from (select rodzaj, min(dataUr) najstarsza,  max(dataUr) najmlodsza from kreatura group by rodzaj) n, kreatura k 
where n.najstarsza=k.dataUr or n.najmlodsza=k.dataUr;

create table uczestnicy as select * from wikingowie.uczestnicy;
create table etapy_wyprawy as select * from wikingowie.etapy_wyprawy;
create table sektor as select * from wikingowie.sektor;      
create table wyprawa as select * from wikingowie.wyprawa;
select * from kreatura k  left join wyprawa w on k.idKreatury = w.id_wyprawy where w.id_wyprawy IS null;
select * from wyprawa;
select * from kreatura;
select * from uczestnicy;
select * from wyprawa w inner join uczestnicy on w.id_wyprawy = u.id_wyprawy inner join ekwipunek e on u.id_uczestnika =e.idEkwipunku;
