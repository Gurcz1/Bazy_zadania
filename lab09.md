DELIMITER //
CREATE TRIGGER kreatura_before_insert
BEFORE INSERT ON kreatura
FOR EACH ROW
BEGIN
  IF NEW.waga <= 0
  THEN
    SET NEW.waga = 1;
  END IF;
END
//
DELIMITER ;
# zadanie 2
select w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa from wyprawa w
inner join kreatura k on k.idKreatury=w.kierownik
where id_wyprawy=old.id_wyprawy;

DELIMITER //
CREATE TRIGGER after_delete_wyprawa
AFTER DELETE ON wyprawa
FOR EACH ROW
BEGIN
  INSERT INTO archiwum_wypraw
(id_wyprawy, nazwa, data_rozpoczecia,data_zakonczenia, kierownik)
  VALUES (OLD.id_wyprawy, old.nazwa,old.data_rozpoczecia, old.data_zakonczenia,(select nazwa from kreatura where idKreatury=old.kierownik));
  end;
  //
  DELIMITER ;
  
  
  
  
  
