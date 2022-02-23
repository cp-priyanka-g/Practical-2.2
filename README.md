# Practical-2.2
Perform queries in MySQL and MongoDb

Step1: docker start  [ID]/[container_name].
       sudo chmod 666 /var/run/docker.sock 

step2: sudo docker exec -it mysql_docker  bash
Step3: mysql -uroot -p 
Enter password: 
Step4: show databases;
step5: use studentDB.

Perform following queriesi n MySQL

1.Create a table named students with fields id, first_name, last_name, standard, percentage, interest, etc... and insert data into it

    mysql> CREATE TABLE Students (ID int NOT NULL PRIMARY KEY,first_name VARCHAR(20), last_name VARCHAR(20),standard int, percentage decimal(3,2),interest decimal(3,2));

    OUTPUT: Select * from Students;
    +----+------------+-----------+----------+------------+----------+
    | ID | first_name | last_name | standard | percentage | interest |
    +----+------------+-----------+----------+------------+----------+
    |  1 | Priyanka   | Gour      |       12 |      54.99 |    10.50 |
    |  2 | Agrima     | Kanodia   |       12 |      34.99 |     4.50 |
    |  3 | Puja       | Bagdi     |       11 |      44.99 |     5.50 |
    |  4 | Anisha     | Shaikh    |       11 |      46.69 |     7.50 |
    |  5 | Amisha     | Shah      |        5 |      45.79 |     8.50 |
    |  6 | Anushka    | Sharma    |        7 |      85.79 |     7.50 |
    |  7 | Anita      | patel     |        8 |      85.00 |     8.50 |
    +----+------------+-----------+----------+------------+----------+
                                                                   

2.Create table student_attendances with fields id, created_at, P/A fields and insert data into it

     mysql> CREATE TABLE Student_attendances (id int NOT NULL PRIMARY KEY,studentID int,created_at DATE,attendance CHAR(100),FOREIGN KEY (studentID) REFERENCES Students(ID));

     OUTPUT: select * from Student_attendances;
    +----+-----------+------------+------------+
    | id | studentID | created_at | attendance |
    +----+-----------+------------+------------+
    |  1 |         1 | 2022-02-02 | P          |
    |  2 |         2 | 2022-02-02 | P          |
    |  3 |         3 | 2022-02-02 | P          |
    |  4 |         4 | 2022-02-02 | A          |
    |  5 |         5 | 2022-02-02 | A          |
    |  6 |         1 | 2022-02-03 | A          |
    |  7 |         1 | 2022-02-04 | P          |
    |  8 |         1 | 2022-02-05 | P          |
    |  9 |         2 | 2022-02-05 | A          |
    | 10 |         2 | 2022-02-06 | P          |
    | 11 |         3 | 2022-02-06 | P          |
    | 12 |         3 | 2022-02-07 | A          |
    | 13 |         4 | 2022-02-07 | P          |
    | 14 |         4 | 2022-02-05 | P          |
    | 15 |         4 | 2022-02-06 | P          |
    | 16 |         2 | 2022-02-03 | P          |
    +----+-----------+------------+------------+
 

3.Prepare queries to find student's presence/absence on a particular day.

    mysql> SELECT * FROM   Students WHERE  ID IN (SELECT id FROM   Student_attendances WHERE  attendance = 'P' AND created_at  = '2022-02-02');

    OUTPUT:
    +----+------------+-----------+----------+------------+----------+
    | ID | first_name | last_name | standard | percentage | interest |
    +----+------------+-----------+----------+------------+----------+
    |  1 | Priyanka   | Gour      |       12 |      54.99 |    10.50 |
    |  2 | Agrima     | Kanodia   |       12 |      34.99 |     4.50 |
    |  3 | Puja       | Bagdi     |       11 |      44.99 |     5.50 |
    +----+------------+-----------+----------+------------+----------+

4.Find total absence/presence of every student.

    mysql> select count(attendance),s.first_name from Student_attendances as a join Students as s on a.studentID=s.id where a.attendance='P' group by a.studentID;

    OUTPUT:
    +-------------------+------------+
    | count(attendance) | first_name |
    +-------------------+------------+
    |                 3 | Priyanka   |
    |                 3 | Agrima     |
    |                 2 | Puja       |
    |                 3 | Anisha     |
    +-------------------+------------+

5.Find absent students with a percentage lower than 70.

    mysql> select count(a.attendance), s.first_name from Student_attendances as a join Students as s on a.studentID=s.id where a.attendance='A' and s.percentage <=70 group by a.studentID;

    OUTPUT:
    +---------------------+------------+
    | count(a.attendance) | first_name |
    +---------------------+------------+
    |                   1 | Anisha     |
    |                   1 | Amisha     |
    |                   1 | Priyanka   |
    |                   1 | Agrima     |
    |                   1 | Puja       |
    +---------------------+------------+              


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

Perform following queries in MongoDB

step1:docker start mongodb
step2:sudo docker exec -it mongodb bash 
    root@be376a33751f:/# mongo



1. Create a collection named students with fields id, first_name, last_name, standard, percentage, interest, etc... and insert data into it

>use studentDB;
>db.Students.insertOne({sid:1,first_name:"Priyanka",last_name:"Gour",standard:12,percentage:99.89,interest:"sports" })

OUTPUT:
{
	"acknowledged" : true,
	"insertedId" : ObjectId("6215bd9b6c5bd456e55bc8fa")
}

>db.Students.find();

OUTPUT:

{ "_id" : ObjectId("6215bd9b6c5bd456e55bc8fa"), "sid" : 1, "first_name" : "Priyanka", "last_name" : "Gour", "standard" : 12, "percentage" : 99.89, "interest" : "sports" }
{ "_id" : ObjectId("6215be716c5bd456e55bc8fd"), "sid" : 3, "first_name" : "Agrima", "last_name" : "Kanodia", "standard" : 11, "percentage" : 53.89, "interest" : "Art" }
{ "_id" : ObjectId("6215bea26c5bd456e55bc8fe"), "sid" : 4, "first_name" : "Swati", "last_name" : "Shah", "standard" : 10, "percentage" : 63.89, "interest" : "Dance" }
{ "_id" : ObjectId("6215c1736c5bd456e55bc8ff"), "sid" : 2, "first_name" : "Shivani", "last_name" : "Singh", "standard" : 10, "percentage" : 89.89, "interest" : "Sports" }
{ "_id" : ObjectId("6215c1986c5bd456e55bc900"), "sid" : 5, "first_name" : "Shivani", "last_name" : "Singh", "standard" : 10, "percentage" : 89.89, "interest" : "Sports" }
{ "_id" : ObjectId("6215c1ce6c5bd456e55bc901"), "sid" : 2, "first_name" : "Puja", "last_name" : "Bagdi", "standard" : 12, "percentage" : 99.89, "interest" : "Music" }


2. Form a query to find students with a percentage lower than 70 and interest in sport.

    > db.Students.find({percentage : { $lt : 70}},{interest:"sports"});

    OUTPUT:
        { "_id" : ObjectId("6215be716c5bd456e55bc8fd"), "interest" : "Art" }
        { "_id" : ObjectId("6215bea26c5bd456e55bc8fe"), "interest" : "Dance" }
        { "_id" : ObjectId("6215c6363050be7f53f58f64"), "interest" : "sports" }


3. Count the total students with a percentage above 70

    > db.Students.find({percentage : { $gt : 70}}).count();
    
    OUTPUT:
    3







    

