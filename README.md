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


	

