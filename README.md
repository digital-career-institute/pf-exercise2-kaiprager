Objective: To comprehend the significance of primary keys and foreign keys in database management, emphasizing their role

Scenario:
Imagine you are designing a database system for a psychology clinic that manages information about patients, psychologists, and their appointments. You'll be working with tables related to patients and psychologists.

Requirements:

Database Management System (DBMS) software (e.g., MySQL, PostgreSQL, SQLite)
Basic SQL knowledge
Tasks:

Create a Table with Private Key and Foreign Key:

Create a table named Patients with the following columns:
PatientID as a private key (representing a unique identifier for each patient)
Other relevant columns like Name, Age, Gender, etc.
Add a foreign key constraint referencing the Psychologists table (Assume a column PsychologistID exists in the Patients table and references the PsychologistID column in the Psychologists table).
Drop Both Keys:

Write SQL commands to drop the primary key constraint and the foreign key constraint from the Patients table.
Add Primary Key:

Alter the Patients table to add a new primary key constraint on the PatientID column.
Add Composite Primary Key:

Create a composite primary key on the PatientID and AppointmentDate columns to uniquely identify appointments (considering the need for appointment scheduling in the future).
Drop Foreign Key:

Remove the foreign key constraint from the Patients table that references the Psychologists table.
Add Foreign Key:

Add a new foreign key constraint on the Patients table, referencing the Psychologists table.

mysql> CREATE DATABASE pf-exercise2;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '-exercise2' at line 1
mysql> 
mysql> CREATE DATABASE pf_exercise2;
Query OK, 1 row affected (0,02 sec)

mysql> USE pf_exercise2;
Database changed
mysql> CREATE TABLE Patients (patientId NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100), age INT, gender VARCHAR(20), appointment DATETIME);
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100), age INT, gender VARCHAR(' at line 1
mysql> CREATE TABLE Patients (patientId NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100), age INT, gender VARCHAR(20));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100), age INT, gender VARCHAR(' at line 1
mysql> CREATE TABLE Patients (patientId INT  NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100), age INT, gender VARCHAR(20), appointment DATETIME);
Query OK, 0 rows affected (0,04 sec)

mysql> drop table patients;
ERROR 1051 (42S02): Unknown table 'pf_exercise2.patients'
mysql> drop table Patients;
Query OK, 0 rows affected (0,02 sec)

mysql> CREATE TABLE Patients (
    ->     PatientID INT AUTO_INCREMENT PRIMARY KEY,
    ->     Name VARCHAR(100),
    ->     Age INT,
    ->     Gender VARCHAR(10),
    ->     PsychologistID INT
    -> );
Query OK, 0 rows affected (0,02 sec)

mysql> ALTER TABLE Patients ADD FOREIGN KEY(PsychologistID) REFERENCES Psychologists(PsychologistID);
ERROR 1824 (HY000): Failed to open the referenced table 'Psychologists'
mysql> CREATE TABLE Psychologists (
    ->     PsychologistID INT AUTO_INCREMENT PRIMARY KEY,
    ->     PsychologistName VARCHAR(100),
    ->     Specialization VARCHAR(100)
    -> );
Query OK, 0 rows affected (0,02 sec)

mysql> ALTER TABLE Patients ADD FOREIGN KEY(PsychologistID) REFERENCES Psychologists(PsychologistID);
Query OK, 0 rows affected (0,06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE Patients;
+----------------+--------------+------+-----+---------+----------------+
| Field          | Type         | Null | Key | Default | Extra          |
+----------------+--------------+------+-----+---------+----------------+
| PatientID      | int          | NO   | PRI | NULL    | auto_increment |
| Name           | varchar(100) | YES  |     | NULL    |                |
| Age            | int          | YES  |     | NULL    |                |
| Gender         | varchar(10)  | YES  |     | NULL    |                |
| PsychologistID | int          | YES  | MUL | NULL    |                |
+----------------+--------------+------+-----+---------+----------------+
5 rows in set (0,00 sec)

mysql> DESCRIBE Psychologists;
+------------------+--------------+------+-----+---------+----------------+
| Field            | Type         | Null | Key | Default | Extra          |
+------------------+--------------+------+-----+---------+----------------+
| PsychologistID   | int          | NO   | PRI | NULL    | auto_increment |
| PsychologistName | varchar(100) | YES  |     | NULL    |                |
| Specialization   | varchar(100) | YES  |     | NULL    |                |
+------------------+--------------+------+-----+---------+----------------+
3 rows in set (0,00 sec)

mysql> INSERT INTO Psychologists (PsychologistName, Specialization)
    -> VALUES
    -> ('Dr. Smith', 'Clinical Psychology'),
    -> ('Dr. Johnson', 'Counseling'),
    -> ('Dr. Williams', 'Child Psychology');
Query OK, 3 rows affected (0,01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO Patients (PatientID, Name, Age, Gender, PsychologistID)
    -> VALUES
    -> (1, 'John Doe', 30, 'Male'),
    -> 
    -> asdfasdfalkj ajsljf
    -> aslkjf a;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'asdfasdfalkj ajsljf
aslkjf a' at line 5
mysql> INSERT INTO Patients (Name, Age, Gender, PsychologistID)
    -> VALUES
    -> ('John Doe', 30, 'Male', 1)
    -> ('Jane Doe', 25 'Female', 2)
    -> ('Donny Blue' 12, 'Male', 3);
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '('Jane Doe', 25 'Female', 2)
('Donny Blue' 12, 'Male', 3)' at line 4
mysql> INSERT INTO Patients (Name, Age, Gender, PsychologistID)
    -> VALUES
    -> ('John Doe', 30, 'Male', 1)
    -> jgrsa hcx
    -> :
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'jgrsa hcx
:' at line 4
mysql> INSERT INTO Patients (Name, Age, Gender, PsychologistID)
    -> VALUES
    -> ('John Doe', 30, 'Male', 1),
    -> ('Jane Doe', 24, 'Female', 2),
    -> ('Donny Bronco', 12, 'Male', 3);
Query OK, 3 rows affected (0,00 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO Psychologists (PsychologistName, Specialization)
    -> VALUES
    -> ('Dr. Smith', 'Clinical Psychology'),
    -> ('Dr. Johnson', 'Counseling'),
    -> ('Dr. Williams', 'Child Psychology');
Query OK, 3 rows affected (0,01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Patients;
+-----------+--------------+------+--------+----------------+
| PatientID | Name         | Age  | Gender | PsychologistID |
+-----------+--------------+------+--------+----------------+
|         1 | John Doe     |   30 | Male   |              1 |
|         2 | Jane Doe     |   24 | Female |              2 |
|         3 | Donny Bronco |   12 | Male   |              3 |
+-----------+--------------+------+--------+----------------+
3 rows in set (0,00 sec)

mysql> SELECT * FROM Psychologists;
+----------------+------------------+---------------------+
| PsychologistID | PsychologistName | Specialization      |
+----------------+------------------+---------------------+
|              1 | Dr. Smith        | Clinical Psychology |
|              2 | Dr. Johnson      | Counseling          |
|              3 | Dr. Williams     | Child Psychology    |
|              4 | Dr. Smith        | Clinical Psychology |
|              5 | Dr. Johnson      | Counseling          |
|              6 | Dr. Williams     | Child Psychology    |
+----------------+------------------+---------------------+
6 rows in set (0,00 sec)

mysql> DELETE FROM Psychologists WHERE PsychologistID = 4;
Query OK, 1 row affected (0,01 sec)

mysql> DELETE FROM Psychologists WHERE PsychologistID = 5;
Query OK, 1 row affected (0,00 sec)

mysql> DELETE FROM Psychologists WHERE PsychologistID = 6;
Query OK, 1 row affected (0,00 sec)

mysql> SELECT * FROM Psychologists;
+----------------+------------------+---------------------+
| PsychologistID | PsychologistName | Specialization      |
+----------------+------------------+---------------------+
|              1 | Dr. Smith        | Clinical Psychology |
|              2 | Dr. Johnson      | Counseling          |
|              3 | Dr. Williams     | Child Psychology    |
+----------------+------------------+---------------------+
3 rows in set (0,00 sec)

mysql> ALTER TABLE Patients DROP PRIMARY KEY;
ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
mysql> ALTER TABLE Patients DROP PRIMARY KEY;
ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
mysql> ALETER TABLE Patients DROP PRIMARY KEY;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'ALETER TABLE Patients DROP PRIMARY KEY' at line 1
mysql> SHOW CREATE TABLE Patients;
+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table    | Create Table                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Patients | CREATE TABLE `Patients` (
  `PatientID` int NOT NULL AUTO_INCREMENT,
  `Name` varchar(100) DEFAULT NULL,
  `Age` int DEFAULT NULL,
  `Gender` varchar(10) DEFAULT NULL,
  `PsychologistID` int DEFAULT NULL,
  PRIMARY KEY (`PatientID`),
  KEY `PsychologistID` (`PsychologistID`),
  CONSTRAINT `Patients_ibfk_1` FOREIGN KEY (`PsychologistID`) REFERENCES `Psychologists` (`PsychologistID`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0,00 sec)

mysql> ALTER TABLE Patients DROP PRIMARY KEY;
ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
mysql> ALTER TABLE Patients ADD PRIMARY KEY(PatientID);
ERROR 1068 (42000): Multiple primary key defined
mysql> ALTER TABLE Patients ADD COLUMN id INT NOT NULL;
Query OK, 0 rows affected (0,02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> UPDATE Patients SET id = PatientID;
Query OK, 3 rows affected (0,01 sec)
Rows matched: 3  Changed: 3  Warnings: 0

mysql> ALTER TABLE Patients DROP COLUMN PatientID;
Query OK, 3 rows affected (0,05 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Patients;
+--------------+------+--------+----------------+----+
| Name         | Age  | Gender | PsychologistID | id |
+--------------+------+--------+----------------+----+
| John Doe     |   30 | Male   |              1 |  1 |
| Jane Doe     |   24 | Female |              2 |  2 |
| Donny Bronco |   12 | Male   |              3 |  3 |
+--------------+------+--------+----------------+----+
3 rows in set (0,00 sec)

mysql> DESCRIBE Patients;
+----------------+--------------+------+-----+---------+-------+
| Field          | Type         | Null | Key | Default | Extra |
+----------------+--------------+------+-----+---------+-------+
| Name           | varchar(100) | YES  |     | NULL    |       |
| Age            | int          | YES  |     | NULL    |       |
| Gender         | varchar(10)  | YES  |     | NULL    |       |
| PsychologistID | int          | YES  | MUL | NULL    |       |
| id             | int          | NO   |     | NULL    |       |
+----------------+--------------+------+-----+---------+-------+
5 rows in set (0,00 sec)

mysql> ALTER TABLE Patients ADD PRIMARY KEY(id);
Query OK, 0 rows affected (0,05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Patients;
+--------------+------+--------+----------------+----+
| Name         | Age  | Gender | PsychologistID | id |
+--------------+------+--------+----------------+----+
| John Doe     |   30 | Male   |              1 |  1 |
| Jane Doe     |   24 | Female |              2 |  2 |
| Donny Bronco |   12 | Male   |              3 |  3 |
+--------------+------+--------+----------------+----+
3 rows in set (0,00 sec)

mysql> ALTER TABLE Patients DROP PRIMARY KEY;
Query OK, 3 rows affected (0,05 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE Patients DROP FOREIGN KEY Patients_ibfk_1;
Query OK, 0 rows affected (0,02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE Patients ADD PRIMARY KEY (id);
Query OK, 0 rows affected (0,05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE Patients ADD PRIMARY KEY (Patient
