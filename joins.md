show databases;

create database museum;

use museum;

show tables;

CREATE TABLE visitor(id INT PRIMARY KEY,name VARCHAR(25) NOT NULL,salary float NOT NULL);


INSERT INTO visitor VALUES (1,'Snehal',500000),(2,'Prasad',550000);


INSERT INTO visitor VALUES (3,'Harshu',350000),(4,'Amar',353240);


SELECT * FROM visitor;



CREATE TABLE booking(bid INT PRIMARY KEY, vid int(10), amount VARCHAR(25) NOT NULL);


INSERT INTO booking VALUES (1,2,200),(2,2,1200),(3,3,2300),(4,4,2100),(5,1,100);


SELECT * FROM booking;

SELECT name,salary,amount FROM visitor LEFT JOIN booking ON vid = booking.vid;

SELECT name,salary,amount FROM visitor RIGHT JOIN booking ON vid = booking.vid;


SELECT name,salary,amount FROM visitor FULL JOIN booking ON id = booking.vid;

SELECT a.id,b.name,a.salary FROM visitor a, visitor b WHERE a.salary > b.salary;


SELECT a.id,b.name,a.salary FROM visitor a, visitor b WHERE a.salary > b.salary;


SELECT id,name,amount FROM visitor,booking;


SELECT id,name,amount FROM visitor,booking;


SELECT name FROM visitor WHERE id IN (SELECT vid FROM booking);


UPDATE visitor SET salary=salary+1000 WHERE id IN (SELECT id FROM booking);


SELECT * FROM visitor;