create database bbb;

use bbb;

CREATE TABLE library (
Book_no INT PRIMARY KEY,
Book_name VARCHAR(255),
author VARCHAR(255)
);

CREATE TABLE library_audit( action_type VARCHAR(50),
Book_no INT,
old_Book_name VARCHAR(50),
old_Author VARCHAR(50)
);

INSERT INTO library(Book_no,Book_name, Author)
VALUES(421,'Maths','Ajay'),(534,'Scince','Robin'),(792,'Physics','Chetan'),(999,'English','Ritesh');

select * from library;

select * from library_audit;

DELIMITER //
CREATE TRIGGER library_update_trigger
BEFORE UPDATE ON library
FOR EACH ROW
BEGIN
INSERT INTO library_audit (action_type,
Book_no,
old_Book_name,
old_Author
)
values('update', OLD.Book_no, old.Book_name,old.Author);
END//

DELIMITER //
CREATE TRIGGER library_delete_trigger
BEFORE DELETE ON library
FOR EACH ROW
BEGIN
INSERT INTO library_audit (action_type,
Book_no,
old_Book_name,
old_Author
)
values('delete', OLD.Book_no, old.Book_name,old.Author);
END//

DELIMITER ;

UPDATE library
SET Book_name = 'Science'
WHERE Book_no = 534;

select * from library_audit ;

DELETE FROM library WHERE Book_no =999;

select * from library_audit ;

DELIMITER //
CREATE TRIGGER library_insert_trigger
AFTER INSERT ON library
FOR EACH ROW
BEGIN
INSERT INTO library_audit (action_type,
Book_no,
old_Book_name,
old_Author
)
values('insert', NEW.Book_no, NEW.Book_name,NEW.Author);
END//
INSERT INTO library(Book_no,Book_name, Author)
VALUES(1001,'History','Vijay');