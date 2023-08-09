# SQL for Student Records Database

**Introduction:**

The purpose of this report is to document the process of designing and implementing a database solution for managing student records. The task involves creating a database named "Students Record" and designing three related tables: "Students Info," "Health Records," and "Performance." Additionally, the report will cover the application of constraints and modifications to ensure data integrity and accuracy.

**Database Design:**
The initial stage of our solution involves the establishment of a database prior to commencing the database design process. We initiated this phase by crafting a student records database and formulating the necessary code to configure the SQL Server for utilization of the newly created database.
```
-- Create the "Students Record" database if it doesn't exist
CREATE DATABASE Students_Record;

-- Switch to the newly created database
USE Students_Record;
```

1. **Students Info Table:**

The next step in the solution was to create the "Students Info" table. This table is designed to store essential information about students, including their unique Student ID, Gender, Name, Age, and Subject. The Student ID was chosen as the primary key to ensure each student has a unique identifier. Constraints were applied to prevent the Student ID and Course from taking null values.
```
-- Create the "Students Info" table
CREATE TABLE Students_Info (
    Student_ID INT IDENTITY(1,1) PRIMARY KEY NOT NULL,
    Gender VARCHAR(10),
    Name VARCHAR(50),
	Age INT,
    Subject VARCHAR(50) NOT NULL
);
```

2. **Health Records Table:**

The second table created was the "Health records" table. This table is linked to the "Students Info" table via the Student ID, forming a relationship between student information and health data. The table contains columns for Blood Group, Height, and Weight. The Student ID was chosen as the foreign key, creating a link between health records and individual students.

```

-- Create the "Health_records" table
CREATE TABLE Health_records (
    Student_ID INT,
    Blood_Group VARCHAR(5),
    Height DECIMAL(5, 2),
    Weight DECIMAL(5, 2),
    FOREIGN KEY (Student_ID) REFERENCES Students_Info (Student_ID)
);

```

3. **Performance Table:**

The "Performance" table was the final table to be created. Similar to the "Health_records" table, it is linked to the "Students Info" table using the Student ID as foreign key. This table stores information about a student's academic performance, including Score and Grade. The Score column has a default value of 0, ensuring that students without a recorded score will automatically get zero score.

```

-- Create the "Performance" table
CREATE TABLE Performance (
    Student_ID INT,
    Score INT DEFAULT 0,
    Grade VARCHAR(2),
	FOREIGN KEY (Student_ID) REFERENCES Students_Info (Student_ID)
);

```

**Constraints and Modifications:**

1. **Constraint for Non-Null Values:**

To ensure data integrity, a constraint was added to the "Students Info" table to prevent the Student ID and Course columns from accepting null values. This helps maintain accurate and complete student records.

2. **Column Name Modification:**

One modification involved changing the column name "Subject" to "Course" in the "Students Info" table. This change enhances clarity and consistency within the database schema.
```
-- Apply modifications
-- Rename the "Course" column to "Subject" in the "Students_Info" table
EXEC sp_rename 'Students_Info.Subject', 'Course', 'COLUMN';
```

3. **Column Removal:**

The "Age" column was removed from the "Students Info" table. Since age can be calculated based on birthdate, removing this column reduces redundancy and simplifies the database structure.
```

-- Drop the "Age" column from the "Students Info" table
ALTER TABLE Students_Info DROP COLUMN Age;
```

**Conclusion:**

In conclusion, the solution involved designing and implementing a database to manage student records efficiently. The "Students Info," "Health records," and "Performance" tables were created, establishing relationships between key pieces of student information. Constraints were applied to ensure data quality, and modifications were made to enhance the schema's clarity and simplicity. This database solution provides a solid foundation for maintaining accurate and organized student records, supporting educational institutions in managing their student data effectively.
