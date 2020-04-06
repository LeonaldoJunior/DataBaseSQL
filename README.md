# DataBaseSQL

MySQL Data Types (Version 8.0)

  INT               -- Whole Numbers
  DECIMAL(M,N)      -- DECIMAL(size, d) size of the digits, d is number after point
                    -- Decimal Numbers - Exact Value
  VARCHAR(l)        -- String of text of length l
  BLOB              -- Binary Large Object, Stores large data
  DATE              -- 'YYYY-MM-DD'
  TIMESTAMP         -- 'YYYY-MM-DD HH:MM:SS' - used for recording events

-- References
-- https://www.w3schools.com/sql/sql_datatypes.asp

The SQL CREATE TABLE Statement

    Syntax:
    CREATE TABLE table_name (
        column1 datatype,
        column2 datatype,
        column3 datatype,
       ....
    );

    Example:
    CREATE TABLE student (
        student_id INT PRIMARY KEY,
        name       VARCHAR(20),
        major      VARCHAR(20)
    );

The SQL DROP TABLE Statement

    Syntax:
    DROP TABLE table_name;

    Example:
    DROP TABLE student;

SQL ALTER TABLE Statement:

  ALTER TABLE - ADD Column:
  
      Syntax:
      ALTER TABLE table_name
      ADD column_name datatype;

      Example:
      ALTER TABLE student 
      ADD gpa DECIMAL;

  ALTER TABLE - DROP COLUMN
  
      Syntax:
      ALTER TABLE table_name
      DROP COLUMN column_name;

      Example:
      ALTER TABLE student 
      DROP COLUMN gpa;

SQL INSERT INTO Statement:

	Syntax:
	INSERT INTO table_name (column1, column2, column3, ...)
	VALUES (value1, value2, value3, ...);

	INSERT INTO table_name
	VALUES (value1, value2, value3, ...);
	
	Example:
	INSERT INTO student
	(student_id, name, major)
	VALUES 
	('1', 'Jack', 'Biology'),
	('2', 'Kate', 'Sociology'),
	('3', 'Claire', 'English'),
	('4', 'Jack', 'Biology'),
	('5', 'Mike', 'Comp. Sci');
	
	Example:
	INSERT INTO student 
	VALUES 
	('1', 'Jack', 'Biology'),
	('2', 'Kate', 'Sociology'),
	('3', 'Claire', 'English'),
	('4', 'Jack', 'Biology'),
	('5', 'Mike', 'Comp. Sci');


The SQL UPDATE Statement
	
	UPDATE Syntax
	UPDATE table_name
	SET column1 = value1, column2 = value2, ...
	WHERE condition;

	Example:
	UPDATE student 
	SET major = 'Bio'
	WHERE major = 'Biology';


The SQL DELETE Statement

	DELETE Syntax:
	DELETE FROM table_name WHERE condition; 

	Example:
	DELETE FROM student
	WHERE student_id = '5';
	
<h3>Criando Banco de Dados</h3>
	
![DataBase](https://user-images.githubusercontent.com/60407200/78585130-b5e8d900-780f-11ea-8d33-a79b173101dc.png)

<h3>Query para criar todas as tabelas</h3>

	CREATE TABLE employee (
	  emp_id INT PRIMARY KEY,
	  first_name VARCHAR(40),
	  last_name VARCHAR(40),
	  birth_day DATE,
	  sex CHAR(1),
	  salary INT,
	  super_id INT,
	  branch_id INT
	);

	CREATE TABLE branch (
	  branch_id INT PRIMARY KEY,
	  branch_name VARCHAR(40),
	  mgr_id INT,
	  mgr_start_date DATE,
	  FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
	);

	ALTER TABLE employee
	ADD FOREIGN KEY(branch_id)
	REFERENCES branch(branch_id)
	ON DELETE SET NULL;

	ALTER TABLE employee
	ADD FOREIGN KEY(super_id)
	REFERENCES employee(emp_id)
	ON DELETE SET NULL;

	CREATE TABLE client (
	  client_id INT PRIMARY KEY,
	  client_name VARCHAR(40),
	  branch_id INT,
	  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE SET NULL
	);

	CREATE TABLE works_with (
	  emp_id INT,
	  client_id INT,
	  total_sales INT,
	  PRIMARY KEY(emp_id, client_id),
	  FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE,
	  FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE
	);

	CREATE TABLE branch_supplier (
	  branch_id INT,
	  supplier_name VARCHAR(40),
	  supply_type VARCHAR(40),
	  PRIMARY KEY(branch_id, supplier_name),
	  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
	);

	SHOW TABLES;
	
<h3>Query para popular todas as tabelas</h3>

	-- Corporate
	INSERT INTO employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL);

	INSERT INTO branch VALUES(1, 'Corporate', 100, '2006-02-09');

	UPDATE employee
	SET branch_id = 1
	WHERE emp_id = 100;

	INSERT INTO employee VALUES(101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, 1);

	-- Scranton
	INSERT INTO employee VALUES(102, 'Michael', 'Scott', '1964-03-15', 'M', 75000, 100, NULL);

	INSERT INTO branch VALUES(2, 'Scranton', 102, '1992-04-06');

	UPDATE employee
	SET branch_id = 2
	WHERE emp_id = 102;

	INSERT INTO employee VALUES(103, 'Angela', 'Martin', '1971-06-25', 'F', 63000, 102, 2);
	INSERT INTO employee VALUES(104, 'Kelly', 'Kapoor', '1980-02-05', 'F', 55000, 102, 2);
	INSERT INTO employee VALUES(105, 'Stanley', 'Hudson', '1958-02-19', 'M', 69000, 102, 2);

	-- Stamford
	INSERT INTO employee VALUES(106, 'Josh', 'Porter', '1969-09-05', 'M', 78000, 100, NULL);

	INSERT INTO branch VALUES(3, 'Stamford', 106, '1998-02-13');

	UPDATE employee
	SET branch_id = 3
	WHERE emp_id = 106;

	INSERT INTO employee VALUES(107, 'Andy', 'Bernard', '1973-07-22', 'M', 65000, 106, 3);
	INSERT INTO employee VALUES(108, 'Jim', 'Halpert', '1978-10-01', 'M', 71000, 106, 3);


	-- BRANCH SUPPLIER
	INSERT INTO branch_supplier VALUES(2, 'Hammer Mill', 'Paper');
	INSERT INTO branch_supplier VALUES(2, 'Uni-ball', 'Writing Utensils');
	INSERT INTO branch_supplier VALUES(3, 'Patriot Paper', 'Paper');
	INSERT INTO branch_supplier VALUES(2, 'J.T. Forms & Labels', 'Custom Forms');
	INSERT INTO branch_supplier VALUES(3, 'Uni-ball', 'Writing Utensils');
	INSERT INTO branch_supplier VALUES(3, 'Hammer Mill', 'Paper');
	INSERT INTO branch_supplier VALUES(3, 'Stamford Lables', 'Custom Forms');

	-- CLIENT
	INSERT INTO client VALUES(400, 'Dunmore Highschool', 2);
	INSERT INTO client VALUES(401, 'Lackawana Country', 2);
	INSERT INTO client VALUES(402, 'FedEx', 3);
	INSERT INTO client VALUES(403, 'John Daly Law, LLC', 3);
	INSERT INTO client VALUES(404, 'Scranton Whitepages', 2);
	INSERT INTO client VALUES(405, 'Times Newspaper', 3);
	INSERT INTO client VALUES(406, 'FedEx', 2);

	-- WORKS_WITH
	INSERT INTO works_with VALUES(105, 400, 55000);
	INSERT INTO works_with VALUES(102, 401, 267000);
	INSERT INTO works_with VALUES(108, 402, 22500);
	INSERT INTO works_with VALUES(107, 403, 5000);
	INSERT INTO works_with VALUES(108, 403, 12000);
	INSERT INTO works_with VALUES(105, 404, 33000);
	INSERT INTO works_with VALUES(107, 405, 26000);
	INSERT INTO works_with VALUES(102, 406, 15000);
	INSERT INTO works_with VALUES(105, 406, 130000);

	show tables;
	SELECT * FROM employee
	SELECT * FROM branch
	SELECT * FROM client
	SELECT * FROM branch_supplier
	SELECT * FROM works_with
	
	
<h3>Banco de Dados Criado</h3>

![DataBaseReal](https://user-images.githubusercontent.com/60407200/78589741-0f083b00-7817-11ea-8cfd-b45becaf5abe.png)

<h3>Algumas queries básicas </h3>
<h4>Find all employees: </h4>

	SELECT * FROM employee;
	
<h4>Resultado: </h4>

![1](https://user-images.githubusercontent.com/60407200/78592687-d74fc200-781b-11ea-97ab-4a6ea021b558.png)

<h4>Find all clients: </h4>

	SELECT * FROM client;

<h4>Resultado: </h4>

![2](https://user-images.githubusercontent.com/60407200/78592693-d7e85880-781b-11ea-89d9-c56c2f137eef.png)

<h4>Find all employees ordered by salary: </h4>

	SELECT * FROM employee
	ORDER BY salary DESC;
	
<h4>Resultado: </h4>

![3](https://user-images.githubusercontent.com/60407200/78592694-d880ef00-781b-11ea-85a0-87dfeb2c94e0.png)

<h4>Find all employees ordered by sex then name: </h4>

	SELECT * FROM employee
	ORDER BY sex, first_name, last_name DESC;
	
<h4>Resultado: </h4>

![4](https://user-images.githubusercontent.com/60407200/78592695-d880ef00-781b-11ea-8616-337922a07e25.png)

<h4>Find the first 5 employees in the table: </h4>

	SELECT * FROM employee
	LIMIT 5;
	
<h4>Resultado: <h4>
	
![5](https://user-images.githubusercontent.com/60407200/78592699-d9198580-781b-11ea-8914-bf017c79c924.png)

<h4>Find the first and last names of all employees: </h4>
	
	SELECT first_name, last_name FROM employee;
	
<h4>Resultado: </h4>

![6](https://user-images.githubusercontent.com/60407200/78592701-d9198580-781b-11ea-8982-2521fb232a5d.png)

<h4>Find the forename and surnames names of all employees: </h4>
	
	SELECT first_name AS forename, last_name AS surname FROM employee;
	
<h4>Resultado: </h4>

![7](https://user-images.githubusercontent.com/60407200/78592702-d9b21c00-781b-11ea-9237-bd767b27362a.png)

<h4>Find out all the different genders: </h4>

	SELECT DISTINCT sex FROM employee;

<h4>Resultado: </h4>

![8](https://user-images.githubusercontent.com/60407200/78592703-da4ab280-781b-11ea-971e-31232968c051.png)	

<h3>Algumas queries básicas com funções </h3>
<h4>Find the number of employees: </h4>

	SELECT COUNT(emp_id) 
	FROM employee;
<h4>Resultado: </h4>

![1](https://user-images.githubusercontent.com/60407200/78598944-9610df80-7826-11ea-874a-73fd9c59d107.png)

<h4>Find the number of female employee born after 1970: </h4>

	SELECT COUNT(emp_id) 
	FROM employee
	WHERE sex = 'F' and birth_day > '1970-01-01';
	
<h4>Resultado: </h4>

![2](https://user-images.githubusercontent.com/60407200/78598932-9315ef00-7826-11ea-9aa2-e303efcd6764.png)

<h4>Find the average of all employee's salaries: </h4>

	SELECT AVG(salary) 
	FROM employee;
	
<h4>Resultado: </h4>

![3](https://user-images.githubusercontent.com/60407200/78598933-93ae8580-7826-11ea-9fc1-9e386a491c24.png)

<h4>Find the average of male employee's salaries: </h4>

	SELECT AVG(salary) 
	FROM employee
	WHERE sex = 'M';
	
<h4>Resultado: </h4>

![4](https://user-images.githubusercontent.com/60407200/78598935-94471c00-7826-11ea-8324-b2c2bea9b24c.png)

<h4>Find the sum of all employee's salaries: </h4>

	SELECT SUM(salary) 
	FROM employee;
	
<h4>Resultado: </h4>

![5](https://user-images.githubusercontent.com/60407200/78598937-94dfb280-7826-11ea-9913-8466d48a563f.png)

<h4>Find out how many males and females there are: </h4>

	SELECT COUNT(sex), sex
	FROM employee
	GROUP BY sex;
	
<h4>Resultado: </h4>

![6](https://user-images.githubusercontent.com/60407200/78598940-95784900-7826-11ea-9acb-612d00e57142.png)

<h4>Find the total sales of each salesman: </h4>

	SELECT SUM(total_sales), emp_id
	FROM works_with
	GROUP BY emp_id;
	
<h4>Resultado: </h4>

![7](https://user-images.githubusercontent.com/60407200/78598943-95784900-7826-11ea-841a-5103604576b1.png)


<h3>Algumas queries básicas com Wildcard </h3>
<h4>Find any client's who are an LLC: </h4>
	
	-- % = any # characters, _ = one character
	SELECT *
	FROM client
	WHERE client_name LIKE '%LLC';
	
<h4>Resultado: </h4>

![1](https://user-images.githubusercontent.com/60407200/78600634-a37b9900-7829-11ea-9b72-da73be20be62.png)

<h4>Find any branch suppliers who are in the label business: </h4>
	
	SELECT *
	FROM branch_supplier
	WHERE supplier_name LIKE '% Label%';
	
<h4>Resultado: </h4>

![2](https://user-images.githubusercontent.com/60407200/78600635-a4142f80-7829-11ea-9382-11a6a5faab81.png)

<h4>Find any employee born on the 10th day of the month: </h4>
	
	SELECT *
	FROM employee
	WHERE birth_day LIKE '_____10%';
	
<h4>Resultado: </h4>

![3](https://user-images.githubusercontent.com/60407200/78600637-a4acc600-7829-11ea-9549-99f87b6337ca.png)

<h4>Find any clients who are schools: </h4>
	
	SELECT *
	FROM client
	WHERE client_name LIKE '%Highschool%';
	
<h4>Resultado: </h4>

![4](https://user-images.githubusercontent.com/60407200/78600639-a4acc600-7829-11ea-95fd-1cdd37f259f7.png)


<h3>Algumas queries básicas com Union </h3>
<h4>Find a list of employee and branch names: </h4>

	SELECT employee.first_name AS Employee_Branch_Names
	FROM employee
	UNION
	SELECT branch.branch_name
	FROM branch;

<h4>Resultado: </h4>

![1](https://user-images.githubusercontent.com/60407200/78604080-9661a880-782f-11ea-9a94-b6a101a5d054.png)

<h4>Find a list of employee and branch names: </h4>

	SELECT salary
	FROM employee
	UNION
	SELECT total_sales
	FROM works_with;

<h4>Resultado: </h4>

![2](https://user-images.githubusercontent.com/60407200/78604089-995c9900-782f-11ea-9770-7260196382ee.png)
