phpMyAdmin is a free software tool written in PHP, intended to handle the administration of MySQL over the Web.

1.	Open phpMyAdmin using the following url http://localhost:port/phpmyadmin

Replace port with the number of the port you are using for your server (80, 8080, or any other). If the port is 80, you can directly access the website without specifying the port number (for example, http://localhost/phpmyadmin).

<img width="1450" height="1318" alt="image" src="https://github.com/user-attachments/assets/460d7282-8e8d-4b13-9418-8c60b4036dfc" />

 

2.	Sign in with the credentials you provided when you installed it (by default, you can sign in with the user root using blank password)

 
3.	Click on the SQL tab, enter the script below and click on Go button in order to create a database and two tables.

<img width="2060" height="1322" alt="image" src="https://github.com/user-attachments/assets/84cd18fb-f966-4822-8648-bb0a7afb141e" />

 
```sql
CREATE DATABASE CompanyDB;

USE CompanyDB;

CREATE TABLE Department (
    Id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL
);

CREATE TABLE Employee (
    Id INT AUTO_INCREMENT PRIMARY KEY,
    Number VARCHAR(50) NOT NULL UNIQUE,
    FirstName VARCHAR(100) NOT NULL,
    LastName VARCHAR(100) NOT NULL,
    DepartmentId INT NOT NULL,
    Position VARCHAR(100) NOT NULL,
    Salary DECIMAL(10, 2) NOT NULL,
    HireDate DATE NOT NULL,
    FOREIGN KEY (DepartmentId) REFERENCES Department(Id) ON DELETE CASCADE
);
```

•	First of all, you are creating a database with the name CompanyDB.
•	The USE statement tells MySQL to use the named database as the default (current) database for subsequent statements.
•	Then, you create a table, Department, with two fields: Id and Name. The Id is set as a primary key with auto-increment, so its value will be handled by MySQL automatically when you insert new data.
•	Finally, you create another table, Employee, with several fields. You set the Id as a primary key with auto-increment, a Number as a unique identifier for the employee, and the DepartmentId field is a foreign key referencing the Id field in the Department table. Last but not the least, the On Delete Cascade ensures that if a department is deleted, all associated employees are also removed (so be careful when deleting a department!).

The picture below indicates a successful execution of the previous script.

<img width="2176" height="1242" alt="image" src="https://github.com/user-attachments/assets/eb719027-d0d2-4473-98ba-114281e4e8f9" />

 

 
4.	Click again on the SQL tab and use the following script to insert data in both tables. Click on the Go button afterwards:

```sql
INSERT INTO Department (Name) VALUES
('IT'),
('Finance'),
('Marketing');

INSERT INTO Employee (Number, FirstName, LastName, DepartmentId, Position, Salary, HireDate) VALUES
('EMP1001', 'Maria', 'Gonzalez', 1, 'Engineer', 72000.00, '2022-06-15'),
('EMP1002', 'John', 'Smith', 2, 'Analyst', 65000.00, '2021-03-22'),
('EMP1003', 'Linda', 'Park', 3, 'Manager', 85000.00, '2020-11-05'),
('EMP1004', 'Carlos', 'Diaz', 1, 'Developer', 68000.00, '2023-01-10'),
('EMP1005', 'Sophia', 'Brown', 2, 'Accountant', 60000.00, '2024-07-18');
```

<img width="2212" height="1306" alt="image" src="https://github.com/user-attachments/assets/3a0e385d-3a3e-4a4d-8474-a043973cff40" />

<img width="2176" height="1044" alt="image" src="https://github.com/user-attachments/assets/cf01276d-c6b2-4091-a8c5-a6a92e610780" />

[< Previous Step](overview.md) | Step 1 | [Next step >](step2.md)

