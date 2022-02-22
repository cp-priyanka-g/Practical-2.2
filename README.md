# Practical-2.2
Perform queries in MySQL and MongoDb
Step1: docker start  [ID].
step2: sudo docker exec -it mysql_docker  bash
Step3: mysql -uroot -p 
Enter password: 
Step4: show databases;
step5: use studentDB.

Perform following queriesi n MySQL

1.Create a table named students with fields id, first_name, last_name, standard, percentage, interest, etc... and insert data into it
    mysql> CREATE TABLE Students (ID int NOT NULL PRIMARY KEY,first_name VARCHAR(20), last_name VARCHAR(20),standard int, percentage decimal(3,2),interest decimal(3,2));

2.Create table student_attendances with fields id, created_at, P/A fields and insert data into it
     mysql> CREATE TABLE Student_attendances (id int NOT NULL PRIMARY KEY,studentID int,created_at DATE,attendance CHAR(100),FOREIGN KEY (studentID) REFERENCES Students(ID));

3.Prepare queries to find student's presence/absence on a particular day.
    SELECT * FROM   Students WHERE  ID IN (SELECT id FROM   Student_attendances WHERE  attendance = 'P' AND created_at  = '2022-02-02');
    +----+------------+-----------+----------+------------+----------+
    | ID | first_name | last_name | standard | percentage | interest |
    +----+------------+-----------+----------+------------+----------+
    |  1 | Priyanka   | Gour      |       12 |      54.99 |    10.50 |
    |  2 | Agrima     | Kanodia   |       12 |      34.99 |     4.50 |
    |  3 | Puja       | Bagdi     |       11 |      44.99 |     5.50 |
    +----+------------+-----------+----------+------------+----------+

4.Find total absence/presence of every student.


5.Find absent students with a percentage lower than 70.

                 


<!-- Students table

mysql> INSERT INTO Students VALUES ('1','Priyanka','Gour','12','54.99','10.50');

mysql> INSERT INTO Students VALUES ('2','Agrima','Kanodia','12','34.99','4.50');

mysql> INSERT INTO Students VALUES ('3','Puja','Bagdi','11','44.99','5.50');

mysql> INSERT INTO Students VALUES ('4','Anisha','Shaikh','11','46.69','7.50');

mysql> INSERT INTO Students VALUES ('5','Amisha','Shah','5','45.79','8.50');

mysql> INSERT INTO Students VALUES ('6','Anushka','Sharma','7','85.79','7.50');

mysql> INSERT INTO Students VALUES ('7','Anita','patel','8','85.00','8.50'); -->

<!--    Student_attendance
 mysql> INSERT INTO Student_attendances VALUES ('1','1','2022-02-02','P');
mysql> INSERT INTO Student_attendances VALUES ('7','1','2022-02-04','P');
mysql> INSERT INTO Student_attendances VALUES ('8','1','2022-02-05','P');
mysql> INSERT INTO Student_attendances VALUES ('6','1','2022-02-03','A');

mysql> INSERT INTO Student_attendances VALUES ('2','2','2022-02-02','P');
mysql> INSERT INTO Student_attendances VALUES ('16','2','2022-02-03','A');
mysql> INSERT INTO Student_attendances VALUES ('9','2','2022-02-05','A');
mysql> INSERT INTO Student_attendances VALUES ('10','2','2022-02-06','P');


mysql> INSERT INTO Student_attendances VALUES ('3','3','2022-02-02','P');
mysql> INSERT INTO Student_attendances VALUES ('11','3','2022-02-06','P');
mysql> INSERT INTO Student_attendances VALUES ('12','3','2022-02-07','A');

mysql> INSERT INTO Student_attendances VALUES ('4','4','2022-02-02','A');
mysql> INSERT INTO Student_attendances VALUES ('13','4','2022-02-07','P');
mysql> INSERT INTO Student_attendances VALUES ('14','4','2022-02-05','P');
mysql> INSERT INTO Student_attendances VALUES ('15','4','2022-02-06','P');

mysql> INSERT INTO Student_attendances VALUES ('5','5','2022-02-02','A'); -->

<!-- Perform following queries in MongoDB

1. Create a collection named students with fields id, first_name, last_name, standard, percentage, interest, etc... and insert data into it
2. Form a query to find students with a percentage lower than 70 and interest in sport.
3. Count the total students with a percentage above 70 -->






    

