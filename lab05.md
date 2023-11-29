# lab5
## Zadanie 1
a)  Usunięcie dwóch najstarszych wikingów (bez Bjorna)
```sql
select * from postac where rodzaj = 'wiking'and nazwa <> 'Bjorn' order by wiek desc limit 2;
delete from postac where rodzaj = 'wiking'and nazwa <> 'Bjorn' order by wiek desc limit 2;
```
b)Usunięcie klucza głównego z tabeli postac
```sql
alter table walizka drop foreign key walizka_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_2;
alter table postac change id_postac id_postac int;
alter table postac drop primary key;
```
## Zadanie 2
a) do tabeli postać dodaj pole pesel składające się z 11 znaków i ustaw to pole na klucz główny 
```sql
alter table postac add column pesel char(11) first;
update postac set pesel='12345678901' + id_postac;
alter table postac change id_postac id_postac int;
alter table postac drop primary key;
alter table przetwory drop foreign key przetwory_ibfk_2;
alter table postac1 add primary key(pesel);
```
b) w tabeli postać zmień pole rodzaj, tak, aby możliwe było dodanie syreny 
```sql
alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena', 'waz');
```
c) wstaw do tabeli syrenę o nazwie Gertruda Nieszczera 
```sql
insert into postac (pesel,id_postac,rodzaj,nazwa,data_ur, wiek) values ('12121212121',10,'syrena', 'Gretuda nieszczera', '1900-01-01', 123);
```
## Zadanie 3
a) Wszystkie postacie, które mają w swojej nazwie 'a', wsadź na statek Bjorna 
```sql
update postac set statek = 'statek1' where nazwa like '%a%';
```
b) Zmniejsz ładowność wszystkim statkom o 30%, których data wodowania była w XX wieku 
```sql
update statek set max_ladownosc=max_ladownosc * 0.7 where year(data_wodowania) between  1901 and 2000;
```
c) ustaw warunek sprawdzający czy wiek postaci nie jest większy od 1000 
```sql
alter table postac add check(wiek <= 1000);
```
## Zadanie 4
a) Do postaci dodaj węża Loko, tylko nie wsadzaj go na statek 
```sql
insert into postac1 values('13131313131', 6, 'Loko', 'waz', '1810-02-10', 213, null, null);
```
b) Stwórz nową tabelę na podstawie tabeli Postacie (dokładnie takie same pola), nazwij ją Marynarz wrzuć do tej tabeli wszystkie postacie które mają zdefiniowany statek 
```sql
CREATE TABLE marynarz like postac;
insert into marynarz select * from postac where statek is not null;
create table marynarz select * from postac where statek is not null;
alter table postac add foreign key (statek) references  statek(nazwa_statku);
```
## Zadanie 5
a) wysadź wszystkich ze statku 
```sql
update postac set statek = null where statek is not null;
```
b) uśmierć jednego wikinga 
```sql
delete from postac where nazwa = 'wiking2';
```
c) zniszcz wszystkie statki 
```sql
delete from statek where nazwa_statku = 'statek2';
delete from statek where nazwa_statku = 'statek1';
```
d) usuń tabelę statek 
```sql
alter table postac1 drop foreign key postac1_ibfk_1;
drop table statek;
```
e) stwórz tabelę zwierz z polami id - klucz główny samo zwiększający się, nazwa - ciąg znaków, wiek liczba
```sql
create table zwierz(id_zwierza INT PRIMARY KEY auto_increment,
nazwa varchar(50),
wiek int);
```
f) przekopiuj z tabeli postac wszystkie zwierzaki 
```sql
INSERT INTO zwierz (nazwa, wiek)SELECT nazwa, wiek FROM postac WHERE rodzaj = 'waz';
INSERT INTO zwierz (nazwa, wiek)SELECT nazwa, wiek FROM postac WHERE rodzaj = 'ptak';
