create table uczestnicy as select * from wikingowie.uczestnicy;
create table etapy_wyprawy as select * from wikingowie.etapy_wyprawy;
create table sektor as select * from wikingowie.sektor;      
create table wyprawa as select * from wikingowie.wyprawa;
select k.nazwa from kreatura k  left join wyprawa w on k.idKreatury = w.id_wyprawy where w.id_wyprawy IS null;
select * from wyprawa;
select * from kreatura;
select * from uczestnicy;
select w.nazwa, sum(e.ilosc) from wyprawa w inner join uczestnicy u on w.id_wyprawy = u.id_wyprawy inner join ekwipunek e on u.id_uczestnika =e.idEkwipunku group by w.nazwa;
#2.2
select w.id_wyprawy, ew.sektor, s.nazwa, ew.kolejnosc, w.data_rozpoczecia, k.nazwa from etapy_wyprawy ew inner join sektor s on ew.sektor = s.id_sektora 
inner join wyprawa w on w.id_wyprawy = ew.idWyprawy 
inner join kreatura k on k.idKreatury =w.kierownik
order by w.data_rozpoczecia asc, ew.kolejnosc asc;

select s.nazwa, count(ew.sektor) from sektor s left join etapy_wyprawy ew on s.id_sektora = ew.sektor group by s.nazwa;

select k.nazwa, if(count(u.id_uczestnika)>0,'bral udzial','nie bral udzialu') from uczestnicy u right join kreatura k on k.idKreatury=u.id_uczestnika group by k.nazwa;

select nazwa, length(nazwa) from kreatura;

select  w.nazwa, sum(length(ew.dziennik))  from wyprawa w inner join etapy_wyprawy ew on w.id_wyprawy=ew.dziennik group by w.nazwa;

select u.id_wyprawy, avg(u.id_uczestnika)/z.waga*e.ilosc from wyprawa w inner join uczestnicy u w.;


select w.nazwa, u.id_uczestnika, e.ilosc, z.waga from uczestnicy u 
inner join ekwipunek e on u.id_uczestnika=e.idKreatury 
inner join zasob z on z.idZasobu=e.idZasobu 
inner join wyprawa w on w.id_wyprawy=u.id_wyprawy
group by w.id_wyprawy;

select w.nazwa, k.nazwa, datediff(w.data_rozpoczecia,k.dataUr) from kreatura k inner join uczestnicy u on u.id_uczestnika=k.idKreatury
inner join wyprawa w on u.id_wyprawy = w.id_wyprawy
inner join etapy_wyprawy ew on ew.idWyprawy=w.id_wyprawy
where ew.sektor=7 group by w.id_wyprawy, k.idKreatury;
