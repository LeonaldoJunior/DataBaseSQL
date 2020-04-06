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

