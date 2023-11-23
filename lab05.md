# lab5
## Zadanie 1
a)
```sql
select * from postac where rodzaj = 'wiking'and nazwa <> 'Bjorn' order by wiek desc limit 2;
delete from postac where rodzaj = 'wiking'and nazwa <> 'Bjorn' order by wiek desc limit 2;
```
b)
```sql
alter table walizka drop foreign key walizka_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_2;
alter table postac change id_postac id_postac int;
alter table postac drop primary key;
```
## Zadanie 2
alter table postac add column pesel char(11) first;
update postac set pesel='12345678901' + id_postac;
alter table postac change id_postac id_postac int;
alter table postac drop primary key;
alter table przetwory drop foreign key przetwory_ibfk_2;
show create table postac;
select * from postac;
desc postac;
alter table postac add column pesel char(11) first;
update postac set pesel='12345678901' + id_postac;
alter table postac1 add primary key(pesel);
alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena', 'waz');
insert into postac (pesel,id_postac,rodzaj,nazwa,data_ur, wiek) values ('12121212121',10,'syrena', 'Gretuda nieszczera', '1900-01-01', 123);
select nazwa from postac where nazwa like '%a%';
# select nazwa from postac where nazwa regexp '[ae]';
update postac set statek = 'statek1' where nazwa like '%a%';
select * from statek where data_wodowania >= '1901-01-01' and data_wodowania <= '2000-12-31';
select * from statek where year(data_wodowania) between  1901 and 2000;
update statek set max_ladownosc=max_ladownosc * 0.7 where year(data_wodowania) between  1901 and 2000;
alter table postac add check(wiek <= 1000);
insert into postac1 values('13131313131', 6, 'Loko', 'waz', '1810-02-10', 213, null, null);
CREATE TABLE marynarz like postac;
desc marynarz;
select * from marynarz;
show create table marynarz;
insert into marynarz select * from postac where statek is not null;
create table marynarz select * from postac where statek is not null;
alter table postac1 add foreign key (statek) references  statek(nazwa_statku);
update postac set statek = null;
create table postac1 select * from marynarz where statek is not null;
select * from postac1;
show create table postac1;
delete from postac1 where nazwa = 'wiking2';
delete from statek where nazwa_statku = 'statek2';
alter table postac1 drop foreign key postac1_ibfk_1;
drop table po
