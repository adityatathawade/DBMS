show databases;
use museum;
create table old_visitor(
    vid INT AUTO_INCREMENT PRIMARY KEY,
    vname VARCHAR(20),
    payment INT
) ; 
insert into old_visitor( vname , payment ) values
( 'Snehal' ,1200) , 
( 'Prasad' , 4561 ) , 
( 'Ayush' , 1230 ) , 
( 'Swaraj' , 9990 ) , 
( 'Advait' , 78890 ) ;
create table new_visitor(
    vid INT AUTO_INCREMENT PRIMARY KEY,
    vname VARCHAR(20),
    payment INT
) ; 
delimiter $$
create procedure add_visitor( in visitor_id int )
begin
declare usrid_2 int;
declare exit_loop boolean;
declare c1 cursor for select vid from old_visitor where vid > visitor_id;
declare continue handler for not found set exit_loop = true;
open c1;
usr_loop: loop
fetch c1 into usrid_2;
if not exists (select * from new_employees where vid = usrid_2) then
insert into new_visitor select * from old_visitor where vid = usrid_2;
end if;
if exit_loop then
close c1;
leave usr_loop;
end if;
end loop usr_loop;
end 
$$
delimiter ;
select * from old_visitor;
select * from new_visitor;
