create table student_marks(
    name varchar(20),
    marks int
); 
create table result(
    name varchar(20),
    rollno int,
    class varchar(20)
);
insert into student_marks(name, marks)
values ('Snehal' , 1000) , 
( 'Prasad' , 990 ) , 
( 'Kaustubh' , 850 ) , 
( 'Swaraj' , 1200 ) , 
( 'Chinmay' , 1300 ) ; 
insert into result(name, class) 
values ( 'Snehal' , '' ) , 
( 'Prasad' , '' ) , 
( 'Kaustubh' , '' ) , 
( 'Swaraj' , '' ) , 
( 'Chinmay' , '' ) ; 
delimiter $$
create procedure proc_grade(in name varchar(20))
begin
declare n varchar(20);
declare m int;
declare category varchar(20) ;
set n = name;
select marks into m from student_marks where student_marks.name = n;
if m >= 990 and m <= 1500 then
    set category = 'distinction';
elseif m >= 989 and m < 990 then
    set category = 'first_class';
elseif m >= 825 and m <= 899 then
    set category = 'high second class';
end if;
update result set class = category where result.name = n;
end
$$
delimiter ;
CALL proc_grade('Snehal');
CALL proc_grade('Prasad');
CALL proc_grade('Kaustubh');
CALL proc_grade('Swaraj');
CALL proc_grade('Chinmay');
select * from student_marks;
select * from result;
